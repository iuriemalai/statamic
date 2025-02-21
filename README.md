## Understanding `$collection->taxonomies()` in Statamic

In Statamic, the `taxonomies` method is used to define or retrieve taxonomies associated with a collection. While the documentation suggests this method works with arrays, it actually returns an `Illuminate\Support\Collection` of `Taxonomy` objects.

### Key Points:
1. **Inspecting Taxonomies:**
   ```php
   Log::info(print_r($collection->taxonomies(), true));
   ```
   This will show a `Collection` of `Taxonomy` objects, not a plain array.

2. **Common Pitfall:**
   The following will not work because taxonomies are returned as objects:
   ```php
   $collectionTaxonomies = $collection->taxonomies();
   $collectionTaxonomies[] = 'new_taxonomy_handle';
   ```

3. **Correct Approach:**
   ```php
   $collectionTaxonomies = $collection->taxonomies()->pluck('handle')->toArray();
   $collectionTaxonomies[] = 'new_taxonomy_handle';
   $collection->taxonomies($collectionTaxonomies);
   $collection->save();
   ```
