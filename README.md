

# Aufgabe 4.1 "Warum erfüllt die Grafik nicht die Standardnormen einer guten Grafik?"
# 1. Keine Achsenbeschriftung, y-Skalierung fehlt komplett und kann nur innerhalb der Grafik durch zwei Werte (2Mrd.€ und 4Mrd.€) erkannt werden
# 2. Farbwahl kontraproduktiv: Farben ähneln sich (drei grüntöne und zwei rottöne) + Menschen mit rot-grüne-Schwäche haben deutliche Probleme, Farben in der Skala zu unterscheiden, für sie wären alle Farben gleich
# 3. Detailierte Beschreibung der einzelnen Balken:
#        a) einerseits zu viel Textinformationen, wodurch es unübersichtlich wird
#        b) andererseits ohne Textinformationen ist die Grafik nicht verständlich genug (kann ohne Textinformationen gar nicht bzw. schwer nur verstanden werden)
# 4. Grafik nicht hundertprozent wertfrei durch positive und negative Smileys, sowieso Textbemerkungen wie: "So 'verdoppelt' die Bundesregierung." "So sähe echte Verdopplung aus"

# Aufgabe 4.2 Zusammenhänge
library(ggplot2)
library(dplyr)

# Grafik 1 Temperatur
ggplot(data = Datensatz_COMET) + 
  geom_point(aes(x = average_temperature, y = count)) +
  ggtitle("Verliehene Fahrräder vs. Temperatur") +
  xlab("durchschnittliche Temperatur") +
  ylab("Ausgeliehende Fahrräder") +
  theme_minimal(13)

# Grafik 2 Niederschlag
ggplot(data = Datensatz_COMET) + 
  geom_point(aes(x = precipitation, y = count)) +
  ggtitle("Verliehene Fahrräder vs. Niederschlag") +
  xlab("Niederschlag") +
  ylab("Ausgeliehende Fahrräder") +
  theme_minimal(13)

# Grafik 3 Windgeschwindigkeit
ggplot(data = Datensatz_COMET) + 
  geom_point(aes(x = windspeed, y = count)) +
  ggtitle("Verliehene Fahrräder vs. Windgeschwindigkeit") +
  xlab("Windgeschwindigkeit in km/h") +
  ylab("Ausgeliehende Fahrräder") +
  theme_minimal(13)

# Grafik 4 Zeit
ggplot(data = Datensatz_COMET) +
  geom_point(aes(x = date, y = count)) +
  ggtitle("Verliehene Fahrräder nach Tagen") +
  xlab("Datum") +
  ylab("Ausgeliehende Fahrräder") +
  theme_minimal(13)

# Aufgabe 4.3 Zusammenhänge Fahrradverleih und Temperatur
# Grafik 1 gefiltert (Regenfreier Tage)
ggplot(data = filter(Datensatz_COMET, precipitation == 0)) +
  geom_point(aes(x = average_temperature, y = count)) +
  ggtitle("Verliehene Fahrräder an regenfreien Tagen") +
  xlab("durchschnittliche Temperatur") +
  ylab("Ausgeliehende Fahrräder") +
  theme_minimal(13)

# Grafik 2 gefiltert (regnerische Tage)
ggplot(data = filter(Datensatz_COMET, precipitation != 0)) +
  geom_point(aes(x = average_temperature, y = count)) +
  ggtitle("Verliehene Fahrräder an regenerischen Tagen") +
  xlab("durchschnittliche Temperatur") +
  ylab("Ausgeliehende Fahrräder") +
  theme_minimal(13)

# Aufgabe 4.4 Verteilungen
# Grafik 1 Fahrradverleih
ggplot(data = Datensatz_COMET) +
  geom_histogram(aes(x = count), col = "black") +
  ggtitle("Verteilung ausgeliehene Fahrräder") +
  xlab("Ausgeliehene Fahrräder") +
  ylab("Beobachtungen")
  theme_minimal(13)

# Grafik 2 Temperatur
ggplot(data = Datensatz_COMET) +
  geom_histogram(aes(x = average_temperature), col = "black") +
  ggtitle("Verteilung der durchschnittlichen Temperatur") +
  xlab("durchschnittliche Temperatur") +
  ylab("Beobachtungen")
  theme_minimal(13)

# Grafik 3 Niederschlag
ggplot(data = Datensatz_COMET) +
  geom_histogram(aes(x = precipitation), col = "black") +
  ggtitle("Verteilung des Niederschlags") +
  xlab("Niederschlagsmenge") +
  ylab("Beobachtungen")
  theme_minimal(13)

# Grafik 4 Windgeschwindigkeit
ggplot(data = Datensatz_COMET) +
  geom_histogram(aes(x = windspeed), col = "black") +
  ggtitle("Verteilung der Windgeschwindigkeit") +
  xlab("Windgeschwindigkeit in km/h") +
  ylab("Beobachtungen")
  theme_minimal(13)

# Aufgabe 4.5 (eine Grafik)
ggplot(data = Datensatz_COMET) +
  geom_histogram(aes(x = count, y = ..density..), alpha = 0.5) +
  geom_density(aes(x = count, color = Season), alpha = 0.8, size = 1) +
  scale_color_manual(values = c("Winter" = "darkblue", "Spring" = "darkgreen", "Summer" = "darkorange", "Autumn" = "black")) +
  ggtitle("Geliehene Fahrräder nach Jahreszeit") +
  xlab("Anzahl ausgeliehener Fahrräder") +
  ylab("Dichte")
  theme_minimal(13)

# Aufgabe 4.6 (eine Grafik)
library(plotly) 
plot_ly(data = Datensatz_COMET,
        x = ~average_temperature,
        y = ~windspeed,
        z = ~count,
        type = "scatter3d",
        mode = "markers",
        marker = list(size = 3, color = ~count, colorscale = 'Viridis', showscale = TRUE))
