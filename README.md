# Data-pipeline-project-
import pandas as pd
import sqlite3

# Step 1: Extract data from CSV
def extract_data(csv_file):
    print("Extracting data...")
    return pd.read_csv(csv_file)

# Step 2: Transform the data
def transform_data(df):
    print("Transforming data...")
    # Example: drop rows with missing values
    df_clean = df.dropna()
    # Example: convert column to lowercase
    if 'name' in df_clean.columns:
        df_clean['name'] = df_clean['name'].str.lower()
    return df_clean

# Step 3: Load the data into SQLite DB
def load_data(df, db_name, table_name):
    print("Loading data into database...")
    conn = sqlite3.connect(db_name)
    df.to_sql(table_name, conn, if_exists='replace', index=False)
    conn.close()
    print("Data loaded successfully.")

# Main function to run pipeline
def run_pipeline():
    csv_file = 'sample_data.csv'  # Replace with your file
    db_name = 'data_pipeline.db'
    table_name = 'cleaned_data'

    data = extract_data(csv_file)
    cleaned_data = transform_data(data)
    load_data(cleaned_data, db_name, table_name)

if __name__ == "__main__":
    run_pipeline()
    
