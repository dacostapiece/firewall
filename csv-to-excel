import pandas as pd

# Replace 'input.csv' with your actual file path
input_csv = 'input.csv'

# Read the CSV file into a DataFrame
df = pd.read_csv(input_csv, header=None, names=["cluster", "sn", "log_type", "xml_log", "raw_id", "update_time"])

# Format the columns as needed
df["cluster"] = df["cluster"].apply(lambda x: x.strip('"') if pd.notna(x) else x)
df["sn"] = df["sn"].apply(lambda x: x.strip('"') if pd.notna(x) else x)
df["log_type"] = df["log_type"].apply(lambda x: x.strip('"') if pd.notna(x) else x)
df["update_time"] = pd.to_datetime(df["update_time"], format='%Y%m%d_%H%M%S', errors='coerce')

# Split the "xml_log" column into multiple columns based on ","
max_elements = df["xml_log"].str.count(',').max() + 1
split_columns = [f"xml_col{i+1}" for i in range(max_elements)]
df[split_columns] = df["xml_log"].str.split(",", expand=True)

# Drop the original "xml_log" column
df.drop(columns=["xml_log"], inplace=True)

# Replace 'output.xlsx' with the desired output Excel file name
output_excel = 'output.xlsx'

# Save the DataFrame to an Excel file
df.to_excel(output_excel, index=False, engine='openpyxl')
