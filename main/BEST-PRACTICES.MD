# prop-kent osztalyszintu arrow function adjunk
-> ne pedig inline-t vagy bind-oltat (kiveve ha constructorban bindoljuk - de ezt keruljuk, mert nem szep megoldas)
-> azert szukseges mert ujrarendelereskor a bind-ok es inline function-ok uj peldanykent vannak kezelve es ezert ujrarenderelodnek az adott komponenssel
-> viszont ha osztalyszintu arrow function hasznalunk, ezek csak akkor renderelodnek ujra ha tartalmaznak olyan state-et vagy prop-ot ami valtozott

## ha masra is akarunk bindolni nem az aktualis this-re, akkor azt a konstruktorban bind-oljunk, ott elerjuk a propokat

# component state es redux state reset az a componentWillUnmount-ban tortenjen
-> mert a componentDidMount elott van egy render, es az hivodjon meg ures state-el
-> ilyenkor a componentDidMount elotti render peldaul jol jon a placeholderek miatt

# csak akkor hasznaljunk state-et ha az kihatassal van a renderre
-> mert a state valtozas ujrarenderelest eredmenyez
