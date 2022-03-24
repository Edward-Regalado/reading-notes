# Create dynamic lists with RecyclerView

- RV makes it easy to dispaly large sets of data.
- supply the data and then define how each item looks, RV library creates teh elements when they're needed
- when elements scroll off screen, RV reuses the view for new items that have scrolled onscreen.
- helps with performance, repsonsiveness and power consumption.

## Key classes

- several different classes work together to bild your dynamic list.
- `RecyclerView is the `ViewGroup` taht contains the views corresponding to your data.
- add RV inot your layout the way you would add any other UI element.
- each individual element in the list is defined by a view obejct.
- the view holder doesn't have any data associated with it when it's created- RV bidns ti to its data.
- The RV requests those views and bind the views to their data by calling methods in the adapter.
- Define the view holder by extending `RecycerView.ViewHolder`
- Define the adapter by extending `RecyclerView.Adapter`
- layout manager arranges the individual elements in your list- can define your own layout or use one of the layout managers provided by the RV.
- layouts are all based on the library's `LayoutManager` abstract class.

## Steps for implementing your RecyclerView

- decide how the list or grid is going to look- you'll be able to use one of the RV library's standard layout managers
- desing how each element in the list is going to look and behave- extend the `ViewHolder` class as it will provide all the functionality.
- definte the `Adapter` that associates your data with the `ViewHolder` views.


## Plan your layout

- RV library provides three layout managers
  - `LinearLayoutManager`: arranges the items in one-dimensional list.
  - `GridLayoutManager`: arranges the tiems in a two-dimensional list.
  - `StaggeredGridLayoutManager`: similar to GLM, but doesn't require items in a row to have the same height or width.

## Implementing your adapter and view holder

- `Adapter` and `ViewHolder` classes work together to define how your data is displayed.
- The `ViewHolder` is a wrapper around a `View` that contains the layout for an individual item in the list.
- The `Adapter` creates the `ViewHolder` object as needed, and also sets the data for those views.

- when you define your adapter, you need to override three key methods:
  - `onCreateViewHolder()`- RV calls this method whenever it needds to create a new VH. It creates and initializes a new view but does not fill it with data.
  - `onBindViewHolder()`- RV calls this method to associate a `ViewHolder` with data. This method fetches data and uses the data to fill the view holder's layout.
  - `getItemCount()`- RV calls this method to get the size of the data set.

```
public class CustomAdapter extends RecyclerView.Adapter<CustomAdapter.ViewHolder> {

    private String[] localDataSet;

    /**
     * Provide a reference to the type of views that you are using
     * (custom ViewHolder).
     */
    public static class ViewHolder extends RecyclerView.ViewHolder {
        private final TextView textView;

        public ViewHolder(View view) {
            super(view);
            // Define click listener for the ViewHolder's View

            textView = (TextView) view.findViewById(R.id.textView);
        }

        public TextView getTextView() {
            return textView;
        }
    }

    /**
     * Initialize the dataset of the Adapter.
     *
     * @param dataSet String[] containing the data to populate views to be used
     * by RecyclerView.
     */
    public CustomAdapter(String[] dataSet) {
        localDataSet = dataSet;
    }

    // Create new views (invoked by the layout manager)
    @Override
    public ViewHolder onCreateViewHolder(ViewGroup viewGroup, int viewType) {
        // Create a new view, which defines the UI of the list item
        View view = LayoutInflater.from(viewGroup.getContext())
                .inflate(R.layout.text_row_item, viewGroup, false);

        return new ViewHolder(view);
    }

    // Replace the contents of a view (invoked by the layout manager)
    @Override
    public void onBindViewHolder(ViewHolder viewHolder, final int position) {

        // Get element from your dataset at this position and replace the
        // contents of the view with that element
        viewHolder.getTextView().setText(localDataSet[position]);
    }

    // Return the size of your dataset (invoked by the layout manager)
    @Override
    public int getItemCount() {
        return localDataSet.length;
    }
}

```

- The layout for each view item is defined in an XML layout file- `text_row_item.xml`

```
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="@dimen/list_item_height"
    android:layout_marginLeft="@dimen/margin_medium"
    android:layout_marginRight="@dimen/margin_medium"
    android:gravity="center_vertical">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/element_text"/>
</FrameLayout>

```

### Sources

[Android for Developers](https://developer.android.com/guide/topics/ui/layout/recyclerview#java)  