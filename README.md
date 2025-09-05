# Tryouts
For Tryouts
# Since there are no missing values we can look for and address outliers

# Visualize outliers with box plots
numerical_cols = ['Inches', 'Weight', 'Price_euros']

plt.figure(figsize=(15, 5))
for i, col in enumerate(numerical_cols):
    plt.subplot(1, 3, i + 1)
    sns.boxplot(y=df[col])
    plt.title(f'Box Plot of {col}')
plt.tight_layout()
plt.show()
# Function to remove outliers using IQR
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    df_cleaned = df[(df[column] >= lower_bound) & (df[column] <= upper_bound)].copy()
    return df_cleaned

# Function to remove outliers using Z-score
def remove_outliers_zscore(df, column, threshold=3):
    z_scores = np.abs((df[column] - df[column].mean()) / df[column].std())
    df_cleaned = df[z_scores < threshold].copy()
    return df_cleaned

# Convert 'Weight' to numeric before outlier removal
df['Weight'] = df['Weight'].str.replace('kg', '').astype(float)


# Apply outlier removal to 'Price_euros' and 'Weight' using IQR
df_cleaned_iqr = remove_outliers_iqr(df, 'Price_euros')
df_cleaned_iqr_weight = remove_outliers_iqr(df_cleaned_iqr, 'Weight')

# Apply outlier removal to 'Inches' using Z-score
df_cleaned = remove_outliers_zscore(df_cleaned_iqr_weight, 'Inches')


print(f"Original shape: {df.shape}")
print(f"Shape after removing outliers: {df_cleaned.shape}")

display(df_cleaned.head())
