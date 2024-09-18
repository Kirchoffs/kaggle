# Notes
#### Read the data
```
train_data_path = '/kaggle/input/california-house-prices/train.csv'
train_df = pd.read_csv(train_data_path)
```

#### Check column data types
```
print(df['Bedrooms'].dtype)

print(df['Bedrooms'].apply(type).unique())
```

#### Distinct values
```
print(train_df['train_data_path'].unique())
print(train_df['train_data_path'].value_counts())
print(train_df['train_data_path'].value_counts().head(10))
print(train_df['Type'].value_counts().get('Apartment'))
```

#### Combine infrequent labels to others
```
valid_types = ['SingleFamily', 'Condo', 'Townhouse', 'MobileManufactured', 'VacantLand', 'Apartment']
train_df.loc[~train_df['Type'].isin(valid_types), 'Type'] = 'Others'
```

#### One-hot encoding based on keywords
```
import re

keywords = {
    'Air forced': r'Air\s+Forced',
    'Central': r'Central',
    'Gas': r'Gas',
    'Furnace': r'Furnace',
    'Wall': r'Wall',
    'Electric': r'Electric'
}

train_df['Heating'] = train_df['Heating'].fillna('')
for keyword in keywords:
    train_df[keyword] = train_df['Heating'].apply(lambda x: 1 if re.search(keywords[keyword], x, flags = re.IGNORECASE) else 0)

train_df.drop(columns = ['Heating'])
```

#### Handle missing numerical values
```
train_df['Lot'] = train_df['Lot'].fillna(train_df['Lot'].mean())
```

```
train_df['Bedrooms'] = pd.to_numeric(train_df['Bedrooms'], errors='coerce')
train_df['Bedrooms'].fillna(train_df['Bedrooms'].mean(), inplace=True)
```

#### Find all non-numeric columns
```
non_numerical_columns = df.select_dtypes(exclude = ['number']).columns
```
