# Hibernate Many to Many

- Many-to-Many relationships is a connection between two types of entities. Both sidse can relate to mutiple instances of the other side.
- Annotate the class with @Entity and the primary key with @id to them proper JPA entities.
- Use the @JoinTable or @JoinColumn attribute connects the owner side of the relatioinship and the inverse colum to the other side.
- On the target side, you only need to provide the name of the field with maps to the relationship @Many-to-Many(mappBy = "name_here")

## Database Setup

- create the employee and project tables along with the employee_project join table with `employee_id` and `project_id` as foreign keys
- afte the DB is setup, prep dependencies and Hibernate config

```
CREATE TABLE `employee` (
  `employee_id` int(11) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(50) DEFAULT NULL,
  `last_name` varchar(50) DEFAULT NULL,
  PRIMARY KEY (`employee_id`)
) ENGINE=InnoDB AUTO_INCREMENT=17 DEFAULT CHARSET=utf8;

CREATE TABLE `project` (
  `project_id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(50) DEFAULT NULL,
  PRIMARY KEY (`project_id`)
) ENGINE=InnoDB AUTO_INCREMENT=18 DEFAULT CHARSET=utf8;

CREATE TABLE `employee_project` (
  `employee_id` int(11) NOT NULL,
  `project_id` int(11) NOT NULL,
  PRIMARY KEY (`employee_id`,`project_id`),
  KEY `project_id` (`project_id`),
  CONSTRAINT `employee_project_ibfk_1` 
   FOREIGN KEY (`employee_id`) REFERENCES `employee` (`employee_id`),
  CONSTRAINT `employee_project_ibfk_2` 
   FOREIGN KEY (`project_id`) REFERENCES `project` (`project_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## The Model Classes

- the model classes Employee and Project need to be created with JPA annotations.
- both Employee and Project classes refer to one another, which means that the association between them is bidirectional.
- in order to map many-to-many association, use the `@ManyToMany`, `@JoinTable` and `@JoinColumn` annotations
- `ManyToMany` annotation is used on both classes to create the relationship.
- the association has two side: the owning side and teh inverse side. In this example, the owning side is the employee side, specified by use the `@JoinTable` annotation in the class.
- `@JoinColumn` used to specify the join/linking column with the main table (employee_id and project_id)

```
@Entity
@Table(name = "Employee")
public class Employee { 
    // ...
 
    @ManyToMany(cascade = { CascadeType.ALL })
    @JoinTable(
        name = "Employee_Project", 
        joinColumns = { @JoinColumn(name = "employee_id") }, 
        inverseJoinColumns = { @JoinColumn(name = "project_id") }
    )
    Set<Project> projects = new HashSet<>();
   
    // standard constructor/getters/setters
}
@Entity
@Table(name = "Project")
public class Project {    
    // ...  
 
    @ManyToMany(mappedBy = "projects")
    private Set<Employee> employees = new HashSet<>();
    
    // standard constructors/getters/setters   
```

## Execution

- wrie the following JUnit test:

```
public class HibernateManyToManyAnnotationMainIntegrationTest {
    private static SessionFactory sessionFactory;
    private Session session;

    // ...

    @Test
    public void givenData_whenInsert_thenCreatesMtoMrelationship() {
        String[] employeeData = { "Peter Oven", "Allan Norman" };
        String[] projectData = { "IT Project", "Networking Project" };
        Set<Project> projects = new HashSet<>();

        for (String proj : projectData) {
            projects.add(new Project(proj));
        }

        for (String emp : employeeData) {
            Employee employee = new Employee(emp.split(" ")[0], 
              emp.split(" ")[1]);
 
            assertEquals(0, employee.getProjects().size());
            employee.setProjects(projects);
            session.persist(employee);
 
            assertNotNull(employee);
        }
    }

    @Test
    public void givenSession_whenRead_thenReturnsMtoMdata() {
        @SuppressWarnings("unchecked")
        List<Employee> employeeList = session.createQuery("FROM Employee")
          .list();
 
        assertNotNull(employeeList);
 
        for(Employee employee : employeeList) {
            assertNotNull(employee.getProjects());
        }
    }

    // ...
}
```
