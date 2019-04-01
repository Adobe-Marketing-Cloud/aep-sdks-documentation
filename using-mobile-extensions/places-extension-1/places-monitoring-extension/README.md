# Places Monitor extension

The Places Monitor extension handles the interactions with the operating system to register and monitor the POIs that are closest to the user. This extension retrieves the POIs that need to be registered from the Places extension and passes the entry and exit notifications to the Places extension. These notifications will be available in Launch rules as events.

The Monitor extension is optional, because some customers might already be monitoring regions with the operating system. If this is the case, ensure that you add the Places extension APIs to receive the nearest POIs from the Places database and to also pass the entry and exit events so that the appropriate actions can be taken.

