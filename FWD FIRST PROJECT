import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }
MONTH_DATA={
    'january' : 1, 'february':2 ,'march':3 , 'april':4 , 'may' : 5, 'june' :6  }

def get_filters():

    
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    while True :
        print('select city you need to analyze chicago , new york city or washington ')
        city=input().lower().strip()
        if city in ['chicago' ,'new york city' , 'washington']:
            break
        print ("Enter a Valid option")
    while True :
        print('select month you need to analyze january february march april may june all ')
        month=input().lower().strip()
        if month in ['january' , 'february' ,'march', 'april' , 'may' , 'june', 'all']:
            break
        print ("Enter a Valid option")
    while True :
        print('select day you need to analyze  monday  tuesday  wednesday thursday  friday  saturday  sunday  all')
        day=input().lower().strip()
        if day in ['monday' , 'tuesday' , 'wednesday' ,'thursday'  ,'friday' , 'saturday' , 'sunday' , 'all']:
            break
            print ("Enter a Valid option")
    # get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    # get user input for month (all, january, february, ... , june)
    # get user input for day of week (all, monday, tuesday, ... sunday)
            

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
    df=pd.read_csv(CITY_DATA[city])
    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['End Time'] = pd.to_datetime(df['End Time'])
    df['month'] = df['Start Time'].dt.month
    df['hour'] = df['Start Time'].dt.hour
    df['day_of_week'] = df['Start Time'].dt.day_name()
    
    
    if month != 'all':
        df = df[df['month'] == MONTH_DATA[month]]
    if day != 'all':
        df = df[df['day_of_week'] == day.title()]
    return df
def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # display the most common month
    print(f"The Most Common Month : {df['month'].mode()[0]} ")
    
    # display the most common day of week
    print(f"The Most Common day : {df['day_of_week'].mode()[0]} ")

    # display the most common start hour
    print(f"The Most Common hour : {df['hour'].mode()[0]} : 00")
    
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)
def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # display most commonly used start station
    print(f"The Most Common start station : {df['Start Station'].mode()[0]} ")


    # display most commonly used end station
    print(f"The Most Common end station : {df['End Station'].mode()[0]} ")

    # display most frequent combination of start station and end station trip
    df['combination start and end']= df['Start Station']+' ==> '+df['End Station']
    print(f"The Most frequent combination of start station and end"
          f"station trip : {df['combination start and end'].mode()[0]} ")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)
 

def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # display total travel time
    #differenceinseconds=pd.Series((df['Start Time'].dt.hour-df['End Time'].dt.hour)*60*60)+df['Start Time'].dt.hour*60+df['Start Time'].dt.second)
    
    #totalsecondend=pd.Series(df['End Time'].dt.hour*60*60+df['End Time'].dt.hour*60+df['end Time'].dt.second)
    totalduration = df['Trip Duration'].sum()
    counts=df.shape[0]
    print(f"total travel time : {totalduration} ")

    # display mean travel time
    print(f"total counts : {counts} ,total mean time : {totalduration/counts}")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()
    

    print(f"counts of Subscriber {df['User Type'].value_counts()[0]} ,counts of Customer {df['User Type'].value_counts()[1]}" )
    if 'Gender' in df:
    # Display counts of gender
        print(f"counts of Males {df['Gender'].value_counts()[0]} ,counts of Females {df['Gender'].value_counts()[1]}" )        
    else:
        print('Gender stats cannot be calculated because Gender does not appear in the dataframe')
    if 'Birth Year' in df:
        # Display earliest, most recent, and most common year of birth
        print(f"earliest year of birth {df['Birth Year'].min()}   ,   "
              f"most recent year of birth {df['Birth Year'].max()}   ,   "
              f"most common year of birth {df['Birth Year'].mode()}")
    else :
        print('Birth Year stats cannot be calculated because Gender does not appear in the dataframe')


    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)
 
def show_data(df):
    view_data = input("Would you like to view 5 rows of individual trip data? Enter yes or no?").lower().strip()
    start_loc = 0
    while (view_data=='yes'):
        print(df.iloc[start_loc:start_loc+5])
        start_loc += 5
        view_data = input("Do you wish to continue?: ").lower().strip()
        if (view_data=='no') :
            break;
         

def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)
        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        show_data(df)
        restart = input('\nWould you like to restart? Enter yes or no.\n').lower().strip()
        if restart.lower() != 'yes':
            break

if __name__ == "__main__":
	main()
