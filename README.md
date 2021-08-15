# Labvanced-t-Column-Fix (eye-tracking data)

> The function (`fix_labvanced_t_column(df)`) checks a (unmodified) Labvanced dataset for missing t values. If t values are missing
the function will fill those using multiple methods.

💡 _NB Labvanced has fixed the issue of missing t values in mid 2021._

**Steps to fill t column**
1. Calculate a median delay value of the time difference for all "times" and "t" values
2. Use that median delay if the dataset has no t value at indexes: `df$t[1]` and `df$t[length(df)$t]`.
3. Sort by times column to get a reasonable estimate about the experiment procedure and to keep NA rows in place
4. Sort _chunk-wise_ t column (_chunks_ are sequential t values surrounded by NA rows)
5. In rare occasions, some chunks that appear later in time may contain t values being smaller then former chunks; if that is the case, a row-wise **bubble sort** is performed, with the aim to keep NA rows in place
6. When t-column chunks are sorted, interpolate t values where t == NA
7. If there were missing values for start and end index, interpolate from start to first valid chunk and likewise for end

**Parameters: `df`**
The function needs an (unmodified) labvanced dataframe (including a `times`, `t`, and `Task_Nr` column)

**Return: `df`**
Returns a dataframe with no missing values in the t column. The dataframe is sorted by t.

**Usage**
fix_labvanced_t_column(df)
