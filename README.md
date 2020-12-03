# vue-assessment-adam-horvath

# Author's comments
I have to admit I had doubts about the requirements given the provided data. I presume that in a real world situation I would have the opportunity to clarify the following requirements:
 - Starting balance
 - Ending balance

As that wasn't an option and since all the transations were marked as 'debit' and also included an 'Available Balance' field of an equal value, I decided to create the following structure to make sense of the data:

    1) Available Balance
        - as we're obviosuly dealing with a debit account, all transactions noted the same available balance and only one of the three was marked as billed with two still pending, I presumed the available balance is set every time a transation is settled. Therefore in the code I filtered the array of transactions to include only settled ones, sorted them by date and grabbed the 'AvailableBalance' property fromt he latest one (such depth obviously wasn't necessary as there is only one Billed transation in my data, but this is a solution that would work with any amount of entries)
    2) Projected Balance
        - As this is a debit account and I presume Available Balance is computed every time a transation is settled, I display a probable current real balance by subtracting all unsettled transactions from Available balance
    3) List of transactions
        - a list of all transactions with their inportant information, some of the columns are sortable

I'm also providing basic responsiveness, limiting the amount of information in the List of transactions on a small screen and adjusting the layout slightly

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
