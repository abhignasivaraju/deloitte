import json
from datetime import datetime

# Function to convert ISO timestamp to milliseconds
def iso_to_milliseconds(iso_timestamp):
    dt = datetime.fromisoformat(iso_timestamp.replace('Z', '+00:00'))
    return int(dt.timestamp() * 1000)

# Function to unify data formats
def unify_data(data1, data2):
    unified_data = []
    for entry in data1:
        unified_entry = {
            'timestamp': iso_to_milliseconds(entry['timestamp']),
            'metric': entry['metric']
        }
        unified_data.append(unified_entry)
    
    for entry in data2:
        unified_entry = {
            'timestamp': entry['timestamp'],
            'metric': entry['metric']
        }
        unified_data.append(unified_entry)
    
    return unified_data

# IMPLEMENT: Finish the load_data function
def load_data():
    with open('data-1.json', 'r') as f1, open('data-2.json', 'r') as f2:
        data1 = json.load(f1)
        data2 = json.load(f2)
    
    unified_data = unify_data(data1, data2)
    
    return unified_data

# IMPLEMENT: Finish the save_data function
def save_data(unified_data):
    with open('data-result.json', 'w') as f:
        json.dump(unified_data, f, indent=2)

if __name__ == "__main__":
    data = load_data()
    save_data(data)
# deloitte
