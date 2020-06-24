# Explore-US-bikeshare
This is my project from Udacity
I have indentation error (outside the loop, unexpected indented...). Dear community, if someone could help?
Here is my code:
import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # TO DO: get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    input_city = input('Please choose one of these cities: Chicago, New York City, Washington\n'.lower())

    while input_city not in ['chicago', 'new york city', 'washington']:

            print('I am not sure what city you are referring to. Please try again!')

city = input('Please choose one of these cities: Chicago, New York City, Washington\n').lower()

    # TO DO: get user input for month (all, january, february, ... , june)
month = input('Please enter the month or ALL \n').lower()

if month in ('january','february','march','april','may','june'):

break

else:
        print('I am not sure what month you are referring to. Please try again!')

month = input('Please enter the month or ALL \n').lower()

    # TO DO: get user input for day of week (all, monday, tuesday, ... sunday)

print('-'*40)
return city, month, day


def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """

# Load file in dataframe
    filename = ('{}.csv'.format(city))
    df = pd.read_csv(filename)

# Convert Starttime to datetime
    df['Start Time'] = pd.to_datetime(df['Start Time'])

# Extract month and day of week from start time
    df['day_of_week'] = df['Start Time'].dt.month
    df['day_of_week'] = df['Start Time'].dt.weekday_name

# Filter by month
# Use index of months to get corresponding list
    if month != 'all':
        months = ['January', 'February', 'March', 'april', 'may', 'june']
        month = months.index(month) + 1

# filter by month to create new frame
    df = df[df['month'] == month]

# filter day of weekly applicable
    if day != 'all':
# filter by day of week to create new dataframe
        df = df[df['day_of_week'] == day.title()]

    return df


def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # TO DO: display the most common month
    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['month'] = df['Start Time'].dt.month
    common_month = df['month'].mode()[0]

    # TO DO: display the most common day of week
    df['day_of_week'] = df['Start Time'].dt.weekday_name
    common_day_of_week = df['day_of_week'].mode()[0]

    # TO DO: display the most common start hour
    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['hour'] = df['Start Time'].dt.hour
    common_hour = df['hour'].mode()[0]

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # TO DO: display most commonly used start station
counts_start_station = df.groupby(['Start Station'])('Start Station').count
sorted_started_station = counts_starts_station.sort_values(ascending = false)
popular_start_station = sorted_start_station.index[0]

    # TO DO: display most commonly used end station
count_end_station = df.groupby(['End Station'])('end Station').count()
sorted_end_station = counts_end_station.sort_values(ascending = False)
popular_end_station = sorted_end_station.index[0]


    # TO DO: display most frequent combination of start station and end station trip
popular_station_combination = df.groupby(['Start Station', 'End Station']).size().nlargest(1)

print("\nThis took %s seconds." % (time.time() - start_time))
print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # TO DO: display total travel time
total_travel_time = df['Trip Duration'].sum() / 60 / 60 / 24
return[total_travel_time]

    # TO DO: display mean travel time
avg_travel_time = df['Trip Duration'].mean / 60
return[avg_travel_time]


print("\nThis took %s seconds." % (time.time() - start_time))
print('-'*40)


def user_stats(df):
    # """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # TO DO: Display counts of user types
user_types = df['User_Type'].value_counts()
print(user_types)

    # TO DO: Display counts of gender
gender_count = df['Gender'].value_counts()
print('The gender count is:', gender_count)

    # TO DO: Display earliest, most recent, and most common year of birth
earliest_year = df['Birth Year'].min()

lastest_year =df['Birth Year'].max()

common_year = df['Birth Year'].count()

print("\nThis took %s seconds." % (time.time() - start_time))
print('-'*40)


def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)

        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break

if __name__ == "__main__":
	main()
