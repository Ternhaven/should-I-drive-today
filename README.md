# drive-or-bike
Information about gasoline and electricity prices in Sweden

## How to use

In Python, it is common to create a virtual environment to which you will download packages. In recent versions of
Python, `virtualenv` is included by default. To make a virtual environment, in the project directory:

```commandline
python -m venv venv
source ./venv/bin/activate
pip install -r requirements.txt
```

On Windows, the second command should be `./venv/Scripts/activate`, and some users might find they need to enter 
`Set-ExecutionPolicy Unrestricted -Scope Process` to run the `activate` script.

## script.py

Simply call `python script.py`. 

![Call the program](images/ss1.png?raw=true "Calling the program")

You will be prompted to enter some data about the distance of your commute, and the efficiency of your e-bike and car.
Entering nothing in these fields will use a default value for [gasoline](https://www.bts.gov/content/average-fuel-efficiency-us-passenger-cars-and-light-trucks)
and for [electricity](https://www.ebikejourney.com/ebike/).

![Running the program](images/ss2.png?raw=true "Running the program")

The program will produce a plot called *circleplot.png*.

![Plot](images/circleplot.png?raw=true "Plot")

## notebook.ipynb

If you'd like to play with the functions, the `notebook.ipynb` Jupyter notebook is friendlier than running the script interactively.
Note that you'd have to [install Jupyter](https://jupyter.org/install):

```commandline
pip install jupyterlab
jupyter-lab
```

The two scraper functions, `electricity_price` and `gasoline_price` each return a number: the current price of electricity (Swedish Krona [SEK] per kilowatt-hour [kWh]) and gasoline (SEK/Liter), respectively.

If we have that
```python
elec_price = electricity_price()
gas_price = gasoline_price()
```

The total cost (in SEK) of a trip of `x` kilometers can then be calculated:
```python
electricity_cost_sek(x, elec_price)  # (For an ebike)
gasoline_cost_sek(x, gas_price)   # (For a car)
```

The function `electricity_cost_sek` assumes a default value of 100 kilometers per kWh efficiency; likewise, `gasoline_cost_sek` assumes a default value of 9.4 kilometers per liter efficiency. Each of these functions can take a third argument if you would like to set either efficiency to a different value, i.e. `electricity_cost_sek(x, elec_price, 80.0)`.
