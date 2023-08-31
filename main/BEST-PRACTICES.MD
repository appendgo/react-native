
# file nevek specifikusak es egyertelmuen leiroak legyenek

* **Bad examples**

* 

* **Good examples**

* 

## leiras

* Peldaul van tobb `fetchClientsAction`-unk a projektben, amik kulonbozokeppen kerik le a client-eket.
  * Ebben az esetben mindegyik `fetchClientsAction`-be tegyuk bele azt a screen vagy modul nevet ahova o tartozik!


# prop-kent osztalyszintu arrow function adjunk

* Don't use inline functions
* Don't use bound functions

-> azert szukseges mert ujrarendelereskor a bind-ok es inline function-ok uj peldanykent vannak kezelve es ezert ujrarenderelodnek az adott komponenssel
-> viszont ha osztalyszintu arrow function hasznalunk, ezek csak akkor renderelodnek ujra ha tartalmaznak olyan state-et vagy prop-ot ami valtozott
-> ha masra is akarunk bindolni nem az aktualis this-re, akkor azt a konstruktorban bind-oljunk, ott elerjuk a propokat

* **Bad example**

```
export default class SingleSelectList extends Component {
  render() {
    return (
      <FlatList
        renderItem={this.renderItem.bind(this)}      // <---------- bound func
        onScrollToIndexFailed={() => {}}             // <---------- inline func
        initialScrollIndex={this.props.selectedIndex}
      />
    );
  }

  renderItem() {
  }
```

* **Good example**

```
export default class SingleSelectList extends Component {
  render() {
    return (
      <FlatList
        renderItem={this.renderItem}                        // <----------
        onScrollToIndexFailed={this.onScrollToIndexFailed}  // <----------
        initialScrollIndex={this.props.selectedIndex}
      />
    );
  }

  renderItem = () => {
  }

  onScrollToIndexFailed = () => {
  }
```

# mapStateToProps hasznalat

* Create only 1 level return object in `mapStoreToProps`
* Use `store` prefix to separate Component state from Redux Store state

* **Bad example**

```
const mapStoreToProps = store => ({
  store: {
    transactions: {
      ...store.transaction.transactions,
        isEmpty:
          store.transaction.transactions.data === null ||
          store.transaction.transactions.data.length === 0,
    },
  },
});
```

* **Good example**

```
const  mapStoreToProps  =  store  => ({
  storeTransactions:  store.transaction.transactions,
  storeIsEmptyTransactions:
    store.transaction.transactions.data  ===  null  ||
    store.transaction.transactions.data.length  ===  0,
});
```

# Reselect library hasznalat

* Kalkulalt ertekek eseteben erdemes hasznalni, pl: `map`, `filter`
* Azert, hogy ezek a kalkulaciok ne fussanak le minden rendernel, csak abban az esetben, ha megvaltoznak a parameterek amelyekbol szamoljuk oket.

```
const selectFilteredClientData = createSelector(
  store => store.appointment.client.clients.searchText,
  store => store.appointment.client.clients.data,
  (searchText, clientData) =>
    clientData.filter(item => {
      let hit = !searchText;

      if (!hit && item.name) {
        hit = normalizeString(item.name).match(new RegExp(searchText, 'gi'));
      }

      if (!hit && item.email) {
        hit = normalizeString(item.email).match(new RegExp(searchText, 'gi'));
      }

      if (!hit && item.phone) {
        hit = normalizeString(item.phone).match(new RegExp(searchText, 'gi'));
      }

      return hit;
    }),
);

const mapStoreToProps = store => ({
  filteredClientData: selectFilteredClientData(store),
  selectedClient: store.appointment.client.selectedClient,
  employeeId: store.appointment.employeeId,
});
```

# Component state es Redux state reset

-> az a componentWillUnmount-ban tortenjen
-> mert a componentDidMount elott van egy render, es az hivodjon meg ures state-el
-> ilyenkor a componentDidMount elotti render peldaul jol jon a placeholderek miatt

# csak akkor hasznaljunk state-et ha az kihatassal van a renderre

-> mert a state valtozas ujrarenderelest eredmenyez
