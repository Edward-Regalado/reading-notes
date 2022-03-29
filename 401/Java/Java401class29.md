# Save data in a lcoal database using Room

- Room persistence library provides an abstraction layer over SQLite to allow fluent database access while using the full power of SQLite.
- compile-time verification of SQL queries
- convenience annotations that minimize repetitive and error-prone boilerplate code.
- streamlined database migration paths


## Setup

- To use Room in your app, add the following dependencies:

```
dependencies {
    def room_version = "2.4.2"

    implementation "androidx.room:room-runtime:$room_version"
    annotationProcessor "androidx.room:room-compiler:$room_version"

    // optional - RxJava2 support for Room
    implementation "androidx.room:room-rxjava2:$room_version"

    // optional - RxJava3 support for Room
    implementation "androidx.room:room-rxjava3:$room_version"

    // optional - Guava support for Room, including Optional and ListenableFuture
    implementation "androidx.room:room-guava:$room_version"

    // optional - Test helpers
    testImplementation "androidx.room:room-testing:$room_version"

    // optional - Paging 3 Integration
    implementation "androidx.room:room-paging:2.5.0-alpha01"
}
```

## Primary components

- 3 major comps in Room:
  - database class that holds the database and serves as the main access point for the underlying connection to your app's persisted data.
  - Data entities that represent tables in your app's database.
  - Data access object (DAOs) that provide methods that your app can use to query, update, insert, and delete data in the databse.
- database class provides your app with instances of the DAOs associated with that database.
- your app can use the DAOs to retrieve data from the database as instances of the associated data entity objects.
- can also upddate rows from the corresponding tables and create new rows for insertion.

## Sample implementation

- `User` entity. Each instance of `User` represents a row in a `user` table in the app's database.

```
@Entity
public class User {
    @PrimaryKey
    public int uid;

    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")
    public String lastName;
}

```

## Data access object (DAO)

- `UserDao` provides the methods that the rest of the app uses to interact with data in the `user` table.

```
@Dao
public interface UserDao {
    @Query("SELECT * FROM user")
    List<User> getAll();

    @Query("SELECT * FROM user WHERE uid IN (:userIds)")
    List<User> loadAllByIds(int[] userIds);

    @Query("SELECT * FROM user WHERE first_name LIKE :first AND " +
           "last_name LIKE :last LIMIT 1")
    User findByName(String first, String last);

    @Insert
    void insertAll(User... users);

    @Delete
    void delete(User user);
}
```

## Database

- this code defines an `AppDatabase` class to hold the database.
- serves's as the app's main access point to the persisted data.
- Database class must satisfy the following conditions:
  - annotated with the `@Database` that includes an `entities` array that lists all of the data entities associated with the database
  - must be an abstract class that extends `RoomDatabase`
  - For each DAO class that is associated with the database, the db class must define an abstract method that has zero args and returns an instance of the DAO class

```
@Database(entities = {User.class}, version = 1)
public abstract class AppDatabase extends RoomDatabase {
    public abstract UserDao userDao();
}
```

## Usage

- afer you've defined the data entity , the DAO and the database object, you can use the following code to create an instance of the database. 

```
AppDatabase db = Room.databaseBuilder(getApplicationContext(),
        AppDatabase.class, "database-name").build();
```

- then use the abstract methods from the `AppDatabase` to get an instance of the DAO.

```
UserDao userDao = db.userDao();
List<User> users = userDao.getAll();
```

# Defining data using Room entities

- when using the Room persistence library to store you app's data, you define entities to represent the objects that you want to store.
- each entity corresponds to a table in the associated Room database, and each instance of an entity represents a row of data in the corresponding table.
- you can use Room entities to define your database schema without writing any SQL code.

```
@Entity
public class User {
    @PrimaryKey
    public int id;

    public String firstName;
    public String lastName;
}
```

- Room uses the class names as the database table name by default.
- set the `tablenName` property of the `@Entity` if you'd like to rename your table.
- Room uses field names as columns names by default.
- add the `@ColumnInfo` annotation to the field and set the `name` property to change the column name.

```
@Entity(tableName = "users")
public class User {
    @PrimaryKey
    public int id;

    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")
    public String lastName;
}
```

## Define a primary key

- each Room entity must define a primary key that uniquely identifies each row in the corresponding database table.
- use the `@PrimaryKey` annotation.

```
@PrimaryKey
public int id;
```

## Define a compostie primary key

- if you need instances of an entity to be uniquely identified by a combination of multiple columns, define a composite primary key by listing those column in the `primaryKey` property of `@Entity`

```
@Entity(primaryKeys = {"firstName", "lastName"})
public class User {
    public String firstName;
    public String lastName;
}
```

## Ignore fields

- Rooom creates a column for each field that's defined in the entity.
- you can choose to ingore and not presist this data by using the `@Ignore` annotation.

```
@Entity
public class User {
    @PrimaryKey
    public int id;

    public String firstName;
    public String lastName;

    @Ignore
    Bitmap picture;
}
```
- when entities inherits fields from a parent, it's easier to use the `ignoredColumns` property of the `@Entity`

```
@Entity(ignoredColumns = "picture")
public class RemoteUser extends User {
    @PrimaryKey
    public int id;

    public boolean hasVpn;
}
```

## Provide table search support

- Room provides different types of annotations that make it easier to search for details in your database.
- use full-text search unles your app's `minSdkVersion` is less than 16.
- if your app requires quick access to db info through full-text search (FTS), have your entities backed by a virtual table that uses eith the FTS3 or FTS4 `SQLite extension module`.
- add the `@Fts3` and `@Fts4` annotations.

```
// Use `@Fts3` only if your app has strict disk space requirements or if you
// require compatibility with an older SQLite version.
@Fts4
@Entity(tableName = "users")
public class User {
    // Specifying a primary key for an FTS-table-backed entity is optional, but
    // if you include one, it must use this type and column name.
    @PrimaryKey
    @ColumnInfo(name = "rowid")
    public int id;

    @ColumnInfo(name = "first_name")
    public String firstName;
}
```

## Index specific columns

- if your app must support SDK version that don't allow FTS3/4, you can still index certain columns in the db to speed up your queries.
- to add indices to an entity, include the `indices` property within the `@Entity` annotation, listing the names of the columns that you want to include in the index or composite index.

```
@Entity(indices = {@Index("name"),
        @Index(value = {"last_name", "address"})})
public class User {
    @PrimaryKey
    public int id;

    public String firstName;
    public String address;

    @ColumnInfo(name = "last_name")
    public String lastName;

    @Ignore
    Bitmap picture;
}
```

- add uniqueness to certain fields in a db by setting the `unique` property of an `@Index` annotation to true.
- prevents a table from having two rows that contain the same set of values for the `firstName` and `lastName` columns:

```
@Entity(indices = {@Index(value = {"first_name", "last_name"},
        unique = true)})
public class User {
    @PrimaryKey
    public int id;

    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")
    public String lastName;

    @Ignore
    Bitmap picture;
}
```

## Include AutoValue-based object

- using the immutable value classes with the `@AutoValue` is helpful when two instances of an entity are considered to be equal if their columns contain identical values.
- when using classes annotated with `@AutoValue` as entities, you can annotate the class's abstract methods using `@PrimaryKey`, `@ColumnInfo`, `@Embedded` and `@Relation`, but you must include the `@CopyAnnotations` each time so that Room can interpret the methods' auto-generated implementations propertly.

```
@AutoValue
@Entity
public abstract class User {
    // Supported annotations must include `@CopyAnnotations`.
    @CopyAnnotations
    @PrimaryKey
    public abstract long getId();

    public abstract String getFirstName();
    public abstract String getLastName();

    // Room uses this factory method to create User objects.
    public static User create(long id, String firstName, String lastName) {
        return new AutoValue_User(id, firstName, lastName);
    }
}
```

## Define relationships between objects

- b/c SQLite is a relational database, you can define relationships between entities.
- Room does not allow this.

### Two approaches

- can model the realtionship using either an intermediate data class with embedded objects, or a relational query method with a multimap return type.

### Intermediate data class

- define a class that models the relationship between your Room entities.
- this data clas holds the pariings between instances of one entity and instance of another entity as `embedded objects`
- query methods can then return instances of this data class for use in your app.

```
@Dao
public interface UserBookDao {
   @Query("SELECT user.name AS userName, book.name AS bookName " +
          "FROM user, book " +
          "WHERE user.id = book.user_id")
   public LiveData<List<UserBook>> loadUserAndBookNames();
}

public class UserBook {
    public String userName;
    public String bookName;
}

```

### Mutimap return types

- you don't need to define any additional data classes.
- you define a `mutimap` return tyep for your method based on the map structure that you want and define the relationship between your entities directly in you SQL query.

```
@Query(
    "SELECT * FROM user" +
    "JOIN book ON user.id = book.user_id"
)
public Map<User, List<Book>> loadUserAndBookNames();

```

- intermediate data class approach allows you to avoid writing complex SQL queries, but it can also result in increased code complexity due to the additional data classes that it requires.
- multimap return type requires your SQL queries to do more work.

## Create embedded objects

- use the `@Embedded` annotation to represent an object that you'd like to decompose into its subfields within a table.
- must query the embedded fields jsut as you would for other individual columns
- `User` class can include a field type of `Address`, which is composed of sub-fields named `street`, `city`, `state` and `postCode`. To sotre the composed columns separately in the table, include an `Address` field in the `User` class that is annotated with `@Embedded`.

```
public class Address {
    public String street;
    public String state;
    public String city;

    @ColumnInfo(name = "post_code") public int postCode;
}

@Entity
public class User {
    @PrimaryKey public int id;

    public String firstName;

    @Embedded public Address address;
}
```

## Define one-to-one relationships

- A one-to-one relationship between to entities is a relationship where each instance of the parent entity corresponds to exactly one instace of the child entity, and vice-versa.
- one-to-one relationship bewteen a `User` and `Library` on a music application.

```
@Entity
public class User {
    @PrimaryKey public long userId;
    public String name;
    public int age;
}

@Entity
public class Library {
    @PrimaryKey public long libraryId;
    public long userOwnerId;
}
```
- to query the list of users and libaries, you must first model the one-to-one relationshipo between the two entities.
- create a new data calss where each instance holds an instance of the parent and child entity.
- add the `@Relation` annotation to the instances of the child entity, with `ParentColumn` set to the name of the primary key column of the parent entity and `entityColumn` set to the name of the column of the child entity that references the parent entity's primary key.

```
public class UserAndLibrary {
    @Embedded public User user;
    @Relation(
         parentColumn = "userId",
         entityColumn = "userOwnerId"
    )
    public Library library;
}
```

- add a method to the DAO class that returns all instances of the data class that pairs the parent and child entity.
- this method requires Room to run two queries, add the `@Transaction` annotation to this method.

```

@Transaction
@Query("SELECT * FROM User")
public List<UserAndLibrary> getUsersAndLibraries();
```

## Define one-to-many relationship

- two entities where each instance of the parent entity corresponds to zero or more instances of the child entity, but each child instance entity can only have exactly one instance to the parent entity.
- For example, a `User` can have multiple `Playlist` on their music app, but each playList is created by only one User.

```

@Entity
public class User {
    @PrimaryKey public long userId;
    public String name;
    public int age;
}

@Entity
public class Playlist {
    @PrimaryKey public long playlistId;
    public long userCreatorId;
    public String playlistName;

    @Transaction
@Query("SELECT * FROM User")
public List<UserWithPlaylists> getUsersWithPlaylists();
}
```

## Definte many-to-many relationships

- relationship between two entities where each instance of the parent corresponds to zero or more instances of the child and vice-versa.

```
@Entity
public class Playlist {
    @PrimaryKey public long playlistId;
    public String playlistName;
}

@Entity
public class Song {
    @PrimaryKey public long songId;
    public String songName;
    public String artist;
}

@Entity(primaryKeys = {"playlistId", "songId"})
public class PlaylistSongCrossRef {
    public long playlistId;
    public long songId;
}

public class PlaylistWithSongs {
    @Embedded public Playlist playlist;
    @Relation(
         parentColumn = "playlistId",
         entityColumn = "songId",
         associateBy = @Junction(PlaylistSongCrossref.class)
    )
    public List<Song> songs;
}

public class SongWithPlaylists {
    @Embedded public Song song;
    @Relation(
         parentColumn = "songId",
         entityColumn = "playlistId",
         associateBy = @Junction(PlaylistSongCrossref.class)
    )
    public List<Playlist> playlists;
}
```

## Define nested relationships

- when you need to query a set of three or more tables that are all related to each other, define nested relationships between the tables.
- if you need to query all the users, all of the playlists for each user and all of the songs in each playlist for each user.

```
@Entity
public class User {
    @PrimaryKey public long userId;
    public String name;
    public int age;
}

@Entity
public class Playlist {
    @PrimaryKey public long playlistId;
    public long userCreatorId;
    public String playlistName;
}
@Entity
public class Song {
    @PrimaryKey public long songId;
    public String songName;
    public String artist;
}

@Entity(primaryKeys = {"playlistId", "songId"})
public class PlaylistSongCrossRef {
    public long playlistId;
    public long songId;
}

public class PlaylistWithSongs {
    @Embedded public Playlist playlist;
    @Relation(
         parentColumn = "playlistId",
         entityColumn = "songId",
         associateBy = Junction(PlaylistSongCrossRef.class)
    )
    public List<Song> songs;
}

@Transaction
@Query("SELECT * FROM User")
public List<UserWithPlaylistsAndSongs> getUsersWithPlaylistsAndSongs();
```

# Accessing data using Room DAOs

- when using Room's persistence libary to store your data, you interact with the stored data by defining data access objects (DAOs).
- each DAO includes methods that offer abstract access to your app's database.
- Room auto-generates implementation of the DAOs you define at compile time.

## Anatomy of a DAO

- define each DAO as either an interface or an abastract class.
- for basic use cases, just use an interface.
- always annotate your DAOs with `@Dao`
- don't have properties, but they do define one or more methods for interacting with the data.

```
@Dao
public interface UserDao {
    @Insert
    void insertAll(User... users);

    @Delete
    void delete(User user);

    @Query("SELECT * FROM user")
    List<User> getAll();
}
```

- there are two types of DAO methods:
  - Convenience methods taht let you insert, update and delete rows in your database without writing any SQL
  - Query methods that let you write your own SQL to interact.

## Insert

- `@Insert` allows you to define methods that insert their parameters into the appropirate table in the database.

```
@Dao
public interface UserDao {
    @Insert(onConflict = OnConflictStrategy.REPLACE)
    public void insertUsers(User... users);

    @Insert
    public void insertBothUsers(User user1, User user2);

    @Insert
    public void insertUsersAndFriends(User user, List<User> friends);
}
```

## Update

- `@Update` allows you to define methods that update specific row in a database table.
- accepts data entity instances as parameters.

```
@Dao
public interface UserDao {
    @Update
    public void updateUsers(User... users);
}
```

## Delete

- `@Delete` allows you to define methods that delete specific rows from a database table.
- accepts data entity instances as parameters.

```
@Dao
public interface UserDao {
    @Delete
    public void deleteUsers(User... users);
}
```

## Query Methods

- `@Query` allows you to write SQl statements and expose them as DAO methods.
- use to query data from you database, or when yuou need to perform more complex inserts, updates and deletes.
- Room validates SQL queries at compile time (if there's issues with your queries, a compilation error occurs).

```
@Query("SELECT * FROM user")
public User[] loadAllUsers();
```

## Return a subset of table's columns

- to save resources and streamline your query's execution, only query the fields that you need.
- Room allows you to return a simple object from any of your queries as long as you can map the set of result columns onto the returned object.

```
public class NameTuple {
    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")
    @NonNull
    public String lastName;
}
@Query("SELECT first_name, last_name FROM user")
public List<NameTuple> loadFullName();
```

### Sources 

[Android](https://developer.android.com/training/data-storage/room)  
[Android](https://developer.android.com/training/data-storage/room/defining-data)  
[Android](https://developer.android.com/training/data-storage/room/relationships)  
[Android](https://developer.android.com/training/data-storage/room/accessing-data#java)  
