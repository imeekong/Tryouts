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
