# GAVI


### Introduzione

In questa esercitazione di "Data Visualization", vi propongo una piccola giuda interattiva di Gavi che, a mio parere, è un piccolo gioiello del basso Piemonte! Qui potrete perdervi tra le stradine del paese e assaggiare i cibi tipici della tradizione piemontese/genovese. Oppure, potete percorrere quello che io chiamo "passeggiata del vino" tra le aziende vinicole (e vi consiglio di farla rigorosamente a piedi o in bici per godervi meglio il paesaggio). Le mie preferite sono le strade che passano da Monterondo o della Lomellina che, in determinati periodi dell'anno (marzo/aprile o settembre/ottobre) sono, a mio parere, uno splendore perchè si riempono di colore grazie ai vigneti! Ma vi consiglio anche di partecipare agli eventi proposti sul sito di Gavi (tra cui **Di Gavi in Gavi**, sito:http://www.comune.gavi.al.it/default.asp). Inoltre, grazie all'aiuto di Google, vi ho riporto l'elenco delle principali aziende vinicole, ristoranti, bar, b&b, hotel e agriturismi.

La giuda è così composta:

- **Dove si trova?**
- **Avvenimenti storici**
- **Monumenti**
- **Gastronomia e Vini** (suddivisa ulteriormente in: **Vini, Gastronomia, Dolci**, con rispettive mappe e elenchi)
- **Dove dormire**

Detto questo, vi auguro una buona Lettura!

PS: Rimango a vostra disposizione per eventuali suggerimenti di miglioramento.


<details>
  <summary>👀 Espandi codice </summary>

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from PIL import Image
from pylab import *
#!pip install folium
import folium
from folium import plugins
#!pip install xlrd
import xlrd   #read file excel
from wordcloud import WordCloud, STOPWORDS

```
</details>

<details>
  <summary>👀 Espandi codice </summary>

```python
# Create Mask Wine
wine_mask = np.array(Image.open("Image/Icon_vino.jpg", 'r'))


# open wine.txt
wine_novel = open('txt_file/wine.txt').read()
stopwords = STOPWORDS

#Word Cloud wine
wine_wc = WordCloud(background_color='white', max_font_size = 88, max_words=3000, mask=wine_mask, stopwords=stopwords).generate(wine_novel)
#wine_wc.recolor(color_func = grey_color_func)
fig = plt.figure()
fig.set_figwidth(8)  # set width
fig.set_figheight(10)  # set height


plt.imshow(wine_wc, interpolation='bilinear')
plt.axis('off')
plt.show()
```
</details>

![Icon_Vino_2](https://github.com/aikibo/GAVI/blob/master/Image/Icon_Vino_2.png)


### Gavi

(/ˈɡavi/, pronunciato [ˈɡaː(v)i] o [ˈɡɔː(v)i] in ligure, Gavi [ˈɡɔvi] in piemontese) o Gavi Ligure (desueto), è un comune della provincia di Alessandria in Piemonte, situato sulla destra del torrente Lemme alla confluenza con il rio Neirone (fonte: https://it.wikipedia.org/wiki/Gavi).

<details>
  <summary>👀 Espandi codice </summary>

```python
gavi = np.array(Image.open('Image/gavi-forte-panorama.jpg'))
fig = plt.figure()
plt.imshow(gavi, interpolation='bilinear')
fig.set_figwidth(14)
fig.set_figheight(18)
plt.axis('off')
plt.show()
```
</details>

![gavi-forte-panorama](https://github.com/aikibo/GAVI/blob/master/Image/gavi-forte-panorama.jpg)

### Stemma

<details>
  <summary>👀 Espandi codice </summary>

```python
gavi = np.array(Image.open('Image/Gavi-Stemma.png'))
fig = plt.figure()
plt.imshow(gavi, interpolation='bilinear')
fig.set_figwidth(5)
fig.set_figheight(6)
plt.axis('off')
plt.show()
```
</details>

![Gavi-Stemma](https://github.com/aikibo/GAVI/blob/master/Image/Gavi-Stemma.png)


# Dove si trova?

Come sudetto, Gavi si trova in provincia di Alessandria. 

**Rispetto alle principali città**

Si trova a:

- **130 km circa da Torino** (circa 1 ora e 40 in macchina, partendo dal centro di Torino)
- **102 km circa da Milano** (circa 1 ora e 30 in macchina, partendo dal centro di Milano)
- **50 km circa da Genova** (circa 1 ora in macchina, partendo dal centro di Genova)

Ma è anche vicino a:

- **13 km circa da Novi Ligure** (circa 20 minuti in macchina): capoluogo del noto cioccolato!
- **10 km circa da Serravalle Scrivia** (circa 15 minuti in macchina): nota per l'Outlet!

<details>
  <summary>👀 Espandi codice </summary>

```python
lat = 44.686270
lng = 8.8071700

# map Gavi
lat_global = [44.686270, 45.0704900, 45.4642700, 44.7624600,44.7227700]
lng_global = [8.8071700, 7.6868200, 9.1895100, 8.7870000, 8.8563500]
labels= ['Gavi','Torino', 'Milano', 'Novi Ligure','Serravalle Scrivia']

gavi_map = folium.Map(location=[lat,lng], zoom_start=8)

mark_gavi = folium.map.FeatureGroup()

#Define the circle marker
for lat_,lng_ in zip(lat_global, lng_global):
    mark_gavi.add_child(
        folium.CircleMarker([lat_,lng_], radius=1, color='red', fill_color='red',fill_opacity=0.3))

gavi_map.add_child(mark_gavi)

#Define the plugin
plugin_gavi = plugins.MarkerCluster().add_to(gavi_map)

for lat_,lng_, label in zip(lat_global, lng_global, labels):
        folium.Marker(location=[lat_, lng_], icon=None, popup=label).add_to(plugin_gavi)

gavi_map.save(outfile= "OUTPUT/gavi_map_main.html")

gavi_map
```
</details>

![Gavi_map](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map.png)


<details>
  <summary>👀 Espandi codice </summary>

```python
# map Gavi
lat = 44.686270
lng = 8.8071700

gavi_map1 = folium.Map(location=[lat,lng], zoom_start=15)

mark_gavi = folium.map.FeatureGroup()
mark_gavi.add_child(folium.CircleMarker(location=[lat,lng], radius=1, color='red', fill_color='red'))
gavi_map1.add_child(mark_gavi)

plugin_gavi1 = plugins.MarkerCluster().add_to(gavi_map1)
folium.Marker([lat, lng], icon=None, popup='Gavi').add_to(plugin_gavi1)

gavi_map1.save(outfile= "OUTPUT/gavi_map.html")

gavi_map1
```
</details>

![Gavi_map1](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map1.png)



# Avvenimenti Storici


<details>
  <summary>👀 Espandi codice </summary>

```python
# Story
gavi = np.array(Image.open('Image/vecchiagavi.jpg'))
fig = plt.figure()
plt.imshow(gavi, interpolation='bilinear')
fig.set_figwidth(14)
fig.set_figheight(18)
plt.axis('off')
plt.show()
```
</details>

![vecchiagavi](https://github.com/aikibo/GAVI/blob/master/Image/vecchiagavi.jpg)


**Avvenimenti storici di Gavi**: 

Le cronache tramandateci parlano di un' antica Gavi in lotta con Roma, poi da questa conquistata. Si cita l' esistenza di un "castello" sulla vetta della roccia di Gavi: in esso, la leggenda vuole che trovasse rifugio dai suoi persecutori la **principessa Gavia**. 

Caduto l' impero romano, Gavi rimase d'ambito bizantino, poi franco. 
Il ritrovamento di resti di armi arabe documenta la presenza dei Saraceni (X secolo): da allora la parte est del monte è denominata appunto **Monte Moro**. 

Notizie storiche certe sul **Castello di Gavi** si hanno verso l' anno Mille. In quel periodo Gavi apparteneva alla famiglia degli **Obertenghi**. Da questi discese il ramo di marchionato che dal XII secolo assunse il titolo 'di Gavi'. Primo marchese di Gavi fu Guido, insediatosi in loco intorno al 1100, il quale nel 1116 cedette il marchesato al figlio Alberto. Durante il lunghissimo dominio di Alberto (60 anni), Gavi, contornata da potenze in netto sviluppo, il vasto comune di Tortona, il Marchesato Aleramico e Genova, e in posizione commercialmente strategica, vide svilupparsi la sua potenza e diventare pedina ambitissima. Gavi si trovò spesso al centro di dispute e di allenze, godendo di un periodo sereno solo durante il dominio dell'imperatore di Svevia Federico I, noto come **Federico Barbarossa**, legato da parentela ed amicizia ai marchesi di Gavi ed in possesso di una torre sul Castello in cui soggiornò più volte. Alla morte del Barbarossa (1190) le sorti del marchesato di Gavi andarono sempre più declinando fino a quando il 16 settembre 1202 con atto ufficiale, passarono ai Genovesi il borgo, il castello e la curia, composta da Tassarolo, Pasturana, Montaldo (Rigoroso), Amelio, Croce e Gottorba, e tutto il loro territorio. 

Da allora le vicende di Gavi e del suo Forte sono strettamente collegate a quelle della **Repubblica di Genova**. 
Nel decennio 1348-1358 Gavi ed il suo Castello furono sotto il dominio della nobile **famiglia dei Visconti**. 

Nel 1359 Gavi ritorna in possesso della Repubblica di Genova seguendone le vicissitudini, fino a quando, tra alterne vicende, ritorna ai Visconti. 
La seconda signoria dei Visconti ha inizio nel 1418, poi il castello viene ceduto ai Fregoso e, nel 1468, alla famiglia dei Guasco di Alessandria. Nel 1528 Gavi e il suo Forte ritornano sotto il dominio della Repubblica di Genova. Si apre finalmente un lungo periodo di pace. 
Nel 1625, durante la guerra tra Genova ed i Franco-Piemontesi, questi assediarono il Forte di Gavi, il quale **resistette strenuamente per 17 giorni** al comando del nobile Alessandro Giustiniano. La battaglia si concluse con la capitolazione del Forte, ma le liti scoppiate in seno ai vincitori, permisero l' arrivo dei soccorsi genovesi, che lo riconquistarono. 
E' in questi anni (1626 - 1929) che il Castello di Gavi assume vero e proprio carattere di fortezza, a seguito dei lavori di ampliamento progettati e diretti da fra Vincenzo di Fiorenzuola. 
Verso la metà del '700 la fortezza di Gavi fu per un breve periodo sotto il dominio austriaco. Infine durante il periodo napoleonico fu teatro di battaglia tra le truppe francesi e quelle austriache. 
In seguito al trattato stipulato tra Francia, Austria ed Inghilterra, nel 1814, la repubblica di Genova fu soppressa ed il suo territorio fu trasferito sotto il dominio del Re di Sardegna Vittorio Emanuele I. Da allora il Forte venne abbandonato e disarmato con decreto del 12 novembre 1854. 

Nella seconda metà del 1800 e fino al 1907 divenne reclusorio penale. **Durante la I e la II guerra mondiale esso funzionò come campo di prigionia militare per austriaci ed inglesi**. 

(fonti: http://www.comune.gavi.al.it/storia.asp)

# Monumenti

Tra i monumenti più caratteristi di Gavi, ve ne elenco solo alcuni(quelli a me più noti!):

- **Forte di Gavi:** Il forte di Gavi è una storica fortezza di tipo prettamente difensivo costruita dai genovesi su un preesistente castello di origine medioevale. È di proprietà demaniale ed è adibito a struttura museale. La fortezza si erge su una rocca naturale a strapiombo sul borgo antico di Gavi. È stata realizzata inglobando un preesistente castello fatto erigere, secondo la leggenda, al tempo delle occupazioni saracene e ungare dalla principessa Gavia (o Gavina) che in quella località aveva stabilito la sua residenza. Secondo la leggenda, la principessa era di origine francese, tanto che ancor oggi il viottolo che conduce al forte, salendo dal borgo, porta il nome di Monserito (da mon cheri).Fuor di leggenda, è difficile stabilire con certezza - a causa della mancanza di riscontri documentari - la data di costruzione dell'originario castello anche se gli studiosi non escludono che vi fosse nell'antichità in quel luogo una fortificazione di epoca pre-romana (fonte: https://it.wikipedia.org/wiki/Forte_di_Gavi).


- **Santuario di N.S. della Guardia:** l santuario di Nostra Signora della Guardia di Gavi in (provincia di Alessandria) è una chiesa dedicata a Nostra Signora della Guardia che sorge sul colle dei Turchini, nei dintorni di Gavi. Il santuario fu eretto nel 1861 in meno di quattro mesi, con la manodopera della popolazione di Gavi e dei paesi circostanti. L'architettura è quella di chiesa a croce greca. Il pavimento è in pregiato marmo rosso Levanto. Ci sono tre altari: uno dedicato al Sacro Cuore di Gesù, l'altro allo sposalizio di Maria Vergine, e l'altare maggiore, sormontato da una nicchia molto bella, che accoglie la statua in legno della Madonna della Guardia (fonte: https://it.wikipedia.org/wiki/Santuario_di_Nostra_Signora_della_Guardia_(Gavi)).


- **Santuario di N.S. Delle Grazie:** Meta per secoli di pellegrinaggi, si presenta oggi, nell'assommarsi di strutture cinque, sei, settecentesche, su quello che fu il quattrocentesco nucleo originale. All' origine dell'attuale complesso edificio vi era un'edicola, attorno alla quale, in seguito al passaggio di San Bernardino da Siena in pellegrinaggio apostolico, fu costruito, intorno al 1450, l'oratorio di San Bernardino, nome che si aggiunse a quello più antico di Santa Maria delle Grazie. Con il tempo sorse un ospizio per i pellegrini che poi diventò convento, nel XVIII secolo si ebbero i lavori di ampliamento e le trasformazioni più imponenti che fecero assumere al Santuario la struttura attuale (fonte: http://www.comune.gavi.al.it/monumenti_oratori.asp). 


- **Portino:** E' l'unica superstite delle quattro porte, di accesso al borgo, di un sistema difensivo basato sulle mura che scendevano dal Forte e che circondavano l'intero abitato di Gavi. La struttura, di inizio XIII secolo, si presenta come una torre a pianta rettangolare, coperta da un tetto a quattro spioventi (benchè si suppone che originariamente la torre non avesse tetto ma terminasse con una merlatura), alleggerita al piano terreno da un'ampia arcata leggermente a sesto acuto, sormontata da una bifora archiacuta con colonnina e capitello corinzio stilizzato.  Il materiale usato per la sua costruzione non e' quello tipico del periodo romanico, l'arenaria locale tagliata e squadrata che si trova negli edifici più antichi della città, bensì la più complessa pietra calcarea (fonte: http://www.comune.gavi.al.it/monumenti_portino.asp).

<details>
  <summary>👀 Espandi codice </summary>

```python
lat = 44.686270
lng = 8.8071700

gavi_map2 = folium.Map(location = [lat,lng], zoom_start = 15)

lat_mon = [44.691273,44.678861, 44.68993716, 44.68871677]
lng_mon = [8.804440,8.787400, 8.81701112, 8.80127192]
popup_mon = ['Forte di Gavi','Santuario di N.S. della Guardia','Santuario di N.S. Delle Grazie', 'Portino']

#create a Feature Group

plugin_gavi2 = plugins.MarkerCluster().add_to(gavi_map2)

#Indicate the popups of each monuments
for lat_, lng_,popup in zip(lat_mon, lng_mon, popup_mon):
    folium.Marker([lat_, lng_], icon = None, popup = popup).add_to(plugin_gavi2)
    
gavi_map2.save(outfile= "OUTPUT/gavi_monumenti.html")

gavi_map2
```
</details>

![Gavi_map2](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map2.png)


# Gastronomia e Vini

**Gavi**, terra di confine tra Liguria a Padania, nel corso della sua storia è passata attraverso molte dominazioni, ma è riuscita a conservare nel tempo, l’autenticità del suo patrimonio di tradizioni: dialetto, costumi, arte culinaria. In posizione strategica sulla strada salaria, granaria, vinaria e pedaggera, fu sempre un luogo di sosta e poterono fiorire bettole e ristori, locande e osterie. Cosa rimane oggi di quella antica, forse un po rustica civiltà del mangiare locale? Senza dubbio molto e lo vediamo subito (fonte: http://www.comune.gavi.al.it/gastronomia.asp). 

### VINI

Oltre al **Cortese di Gavi**, sviluppatosi specialmente nella seconda metà del secolo scorso, in queste zone si sono sempre prodotti e consumati **Dolcetto e barbera**, vini che venivano versati anche nelle zuppe e minestre, non esclusi i ravioli, che a Gavi ebbero i natali. 

#### Caratteristiche del Cortese di Gavi:

**Vitigno**: cortese

**Colore**: paglierino più o meno tenue con riflessi verdognoli.

**Profumo**: delicato; ha sentore di frutta fresca

**Sapore**: asciutto, pieno, gradevole di gusto fresco e armonico.

**Gradazione Minima Naturale**: 10%

**Gradazione Alcolica Minima Complessiva**: 10.5%

**Resa massimo per ha**: 100q.

**Resa massimo di uva in vino**: 70%

**Acidità Totale Minima**: 5

**Invecchiamento**: per legge non prescritto, da bersi preferibilmente giovane.

**Riconoscimenti**: 1974 D.O.C.; 1998 D.O.C.G.

(Viene prodotto anche nel tipo spumante) 

Con il riconoscimento della **DOCG**, nel 1998, il Gavi ha completato il percorso che lo ha reso famoso in tutto il mondo. I primi impianti razionali in grande stile di Cortese, vitigno autoctono gia' citato nel Seicento, sono dovuti alla famiglia dei Cambiaso nelle tenute Centuriona e Toledana nel 1876, grazie alla buona qualita' del vino ottenuto, l'esempio fu presto seguito dalle altre grandi tenute della zona. L'affermazione del Cortese di Gavi, la specializzazione vitivinicola, la spinta qualitativa e promozionale delle grandi aziende portarono al riconoscimento, nel 1974 della DOC e alla recente DOCG. Attualmente la ricerca enologica delle grandi aziende e' rivolta a produrre, oltre al classico bianco profumato e fresco, vini piu' strutturati e longevi, di impronta 'francese' (fonte: http://www.comune.gavi.al.it/vinogavi.asp).

#### Dove comprare il vino: 

Vi consiglio di consultare i seguenti links:

- http://www.produttoridelgavi.com 
- http://www.consorziogavi.com

Sotto trovate la mappa delle aziende vinicole della zona e il rispettivo elenco.

<details>
  <summary>👀 Espandi codice </summary>

```python
#Map of restaurants

gavi_vini = pd.read_excel('XLSX/Gavi_Vini.xlsx')
df_vini = pd.DataFrame(gavi_vini,columns = ['Aziende_Vinicole','Indirizzo','Telefono','Lat','Lng'])
gavi_vini.drop(columns=['Lat','Lng'], inplace=True)

lat_vini = df_vini.Lat
lng_vini = df_vini.Lng
labels = df_vini['Aziende_Vinicole']

gavi_map3 = folium.Map(location=[lat,lng], zoom_start=12)

plugin_gavi3 = plugins.MarkerCluster().add_to(gavi_map3)
for lat_,lng_,label in zip(lat_vini,lng_vini,labels):
       folium.Marker(location=[lat_, lng_], icon=None, popup=label).add_to(plugin_gavi3)

gavi_map3.save(outfile= "OUTPUT/gavi_aziende_vinicole.html")

gavi_map3
```
</details>

![Gavi_map3](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map3.png)


```python
gavi_vini
```


![Gavi_tab_vini](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_tab_vini.png)



### GASTRONOMIA

I **ravioli**, dal ripieno di carni bovine e suine, legati con uova, formaggio, borragine e scarola, dalla sfoglia sapientemente sottile, si mangiano anche con il “tocco” il locale sugo di carne, oltre che col solo formaggio e al naturale. 

Famose anche le carni caprine e ovine in umido, accompagnate da patate e legumi, i salamini con fagioli e i piatti di trippa e fave. Taglierini e lavagnette, chiamati anche stringoni, sono esaltati da sughi di funghi, lepre, salsicce con piselli, di pomodoro e origano, di basilico e aglio, cioè il pesto. I minestroni variano secondo le stagioni, sempre ricchi e densi abbastanza da mantenere ritto il cucchiaio. 

Altra prerogativa locale, sono le **focacce**: **celebre quella stirata, oliata e salata del mattino e quella con patate del pomeriggio**. Grande è la varietà di torte, dalla verde a quella di riso, dalla Pasqualina a quella di bietole (gè). Oltre i fritti nella “negia” (ostia) i fritti di latte brusco e di verdure varie con fegato e animelle costituiscono un “misto” non necessariamente pesante. 

Varie anche le frittate, da quelle al papavero, all’ortica, all’asparago selvatico, allo zucchino. 

Un **piatto rustico** sono le lasagne ben condite di olio e formaggio con pancetta, fagioli e ceci; dalla farina di questo ultimo nascono le farinate e paniccie fritte. 

Particolarità locale sono poi i gnocchetti, una insuperabile pasta per brodo con fegatini. I **funghi** qui si cucinano bene al forno con le patate, come pure il capretto con i carciofi. 

Oltre ai colli di volatili ripieni, abituale è a Gavi la **cima** ed il **pollo e coniglio in casseruola**. 

Il r**isotto al Gavi** i non deve far dimenticare il riso con piselli, carciofi, salsiccia, filoni e funghi secchi completato al forno. 

A ricordo dei tempi in cui a Gavi arrivava il pesce azzurro, restano acciughe e sardine ripiene al tegame, o gli sgombri in umido, e pesce gaviese, anche se viene da lontano, è lo stoccafisso accomodato o all’ulivo. 

**L’ insaccato principe di Gavi resta la suina “testa in cassetta”**. 

(fonte: http://www.comune.gavi.al.it/gastronomia.asp)

#### Dove andare a mangiare

<details>
  <summary>👀 Espandi codice </summary>

```python
#Map of restaurants
gavi_risto = pd.read_excel('XLSX/Gavi_Ristoranti.xlsx')
df_risto = pd.DataFrame(gavi_risto,columns = ['Ristoranti','Indirizzo','Telefono','Lat','Lng'])
gavi_risto.drop(columns=['Lat','Lng'], inplace=True)

lat_risto = df_risto.Lat
lng_risto = df_risto.Lng
labels = df_risto.Ristoranti

gavi_map4 = folium.Map(location=[lat,lng], zoom_start=15)

plugin_gavi4 = plugins.MarkerCluster().add_to(gavi_map4)
for lat_,lng_,label in zip(lat_risto,lng_risto,labels):
       folium.Marker(location=[lat_, lng_], icon=None, popup=label).add_to(plugin_gavi4)
        
#Map of bar
gavi_bar = pd.read_excel('XLSX/GAVI_BAR.xlsx')
df_bar = pd.DataFrame(gavi_bar,columns = ['Bar/Pasticceria','Indirizzo','Telefono','Lat','Lng'])
gavi_bar.drop(columns=['Lat','Lng'], inplace=True)

lat_bar = df_bar.Lat
lng_bar = df_bar.Lng
labels_bar = df_bar['Bar/Pasticceria']

gavi_map5 = folium.Map(location=[lat,lng], zoom_start=15)

plugin_gavi5 = plugins.MarkerCluster().add_to(gavi_map5)
for lat_,lng_,label in zip(lat_bar,lng_bar,labels_bar):
       folium.Marker(location=[lat_, lng_], icon=None, popup=label).add_to(plugin_gavi5)
        
#Map of B&B
gavi_bb = pd.read_excel('XLSX/GAVI_DORMIRE.xlsx')
df_bb = pd.DataFrame(gavi_bb,columns = ['Dove_dormire','Indirizzo','Telefono','Lat','Lng'])
gavi_bb.drop(columns=['Lat','Lng'], inplace=True)

lat_bb = df_bb.Lat
lng_bb = df_bb.Lng
labels_bb = df_bb['Dove_dormire']

gavi_map6 = folium.Map(location=[lat,lng], zoom_start=15)

plugin_gavi6 = plugins.MarkerCluster().add_to(gavi_map6)
for lat_,lng_,label in zip(lat_bb,lng_bb,labels_bb):
       folium.Marker(location=[lat_, lng_], icon=None, popup=label).add_to(plugin_gavi6)
```
</details>

```python
#Map of restaurants

gavi_map4.save(outfile= "OUTPUT/gavi_ristoranti.html")

gavi_map4
```



![Gavi_map4](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map4.png)



```python
gavi_risto
```

![Gavi_tab_risto](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_tab_risto.png)

### DOLCI

Ricca è anche la **tradizione dolciaria**: ricordiamo i canestrelletti di pasta frolla, le schiumette, il pandolce, il latte di gallina, i malfatti al miele e cortese ed i supremi **amaretti di Gavi**. 


(fonti: http://www.comune.gavi.al.it/gastronomia.asp![image.png](attachment:image.png)

#### Dove andare:


```python
#Map of bar

gavi_map5.save(outfile= "OUTPUT/gavi_bar.html")

gavi_map5
```

![Gavi_map5](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map5.png)

```python
gavi_bar
```

![Gavi_tab_bar](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_tab_bar.png)


```python
#Map of bar
gavi_map.save(outfile= "OUTPUT/gavi_bb.html")

gavi_map6
```

![Gavi_map6](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_map6.png)


```python
gavi_bb
```
![Gavi_tab_bb.png](https://github.com/aikibo/GAVI/blob/master/Image/Gavi_tab_bb.png)
