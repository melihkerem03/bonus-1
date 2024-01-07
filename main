# Task-1: Load historical data from orcl.csv into a list of dictionaries

# Open the file in read mode
with open("orcl.csv", "r") as file:
    # Read all lines from the file
    lines = file.readlines()

# Extract column headers from the first line
headers = lines[0].strip().split(',')

# Initialize an empty list to store data as dictionaries
data_list = []

# Loop through the remaining lines and create a dictionary for each row
for line in lines[1:]:
    values = line.strip().split(',')
    # Create a dictionary by zipping headers and values
    data_dict = dict(zip(headers, values))
    # Append the dictionary to the data_list
    data_list.append(data_dict)

# Task-2: Calculate Simple Moving Averages (SMA) and Relative Strength Index (RSI)

# Initialize variables for SMA and RSI calculations
sma_values = []
rsi_values = []
closing_prices = [float(data['Close']) for data in data_list]

# Calculate SMA for a 5-day window
for i in range(4, len(data_list)):
    sma = sum(closing_prices[i-4:i+1]) / 5
    sma_values.append(sma)

# Calculate RSI for a 14-day window
for i in range(14, len(data_list)):
    gains = [closing_prices[j+1] - closing_prices[j] for j in range(i-13, i) if closing_prices[j+1] > closing_prices[j]]
    losses = [-1 * (closing_prices[j+1] - closing_prices[j]) for j in range(i-13, i) if closing_prices[j+1] < closing_prices[j]]

    average_gain = (sum(gains) / 14) if gains else 0
    average_loss = (sum(losses) / 14) if losses else 0

    if average_loss != 0:
        relative_strength = average_gain / average_loss
        rsi = 100 - (100 / (1 + relative_strength))
    else:
        rsi = 100

    rsi_values.append(rsi)

# Task-3: Write SMA to orcl-sma.csv and RSI to orcl-rsi.csv

# Write SMA values to orcl-sma.csv
with open("orcl-sma.csv", "w") as sma_file:
    sma_file.write("Date,SMA\n")
    for i in range(4, len(data_list)):
        sma_file.write(f"{data_list[i]['Date']},{sma_values[i-4]:.2f}\n")

# Write RSI values to orcl-rsi.csv
with open("orcl-rsi.csv", "w") as rsi_file:
    rsi_file.write("Date,RSI\n")
    for i in range(14, len(data_list)):
        rsi_file.write(f"{data_list[i]['Date']},{rsi_values[i-14]:.2f}\n")
