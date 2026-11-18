# Lab 6 : Afficher une grande liste avec SectionList (My Restaurant)

- **URL de la plateforme** : https://mliaedu.toubkalit.com/student/courses/38/labs/243
- **Formation** : React Native

---

## 1. Objectifs pédagogiques
À la fin de ce TP, l’étudiant sera capable de :
- Structurer des données en **sections** pour `SectionList` ;
- Utiliser les props principales de `SectionList` : `sections`, `renderItem`, `renderSectionHeader`, `keyExtractor` ;
- Afficher, pour chaque élément, **nom + prix** sur une ligne ;
- Ajouter un style cohérent pour obtenir un rendu proche de la maquette.

---

## 2. Étape 1 : Création du projet
```bash
npx create-expo-app my-restaurant-sectionlist
cd my-restaurant-sectionlist
npx expo start
```

---

## 3. Étape 2 : Préparer la structure des fichiers
```text
my-restaurant-sectionlist/
  components/
    AppHeader.js
    AppFooter.js
    MenuItems.js
  App.js
```

---

## 4. Étape 3 : Créer l’en-tête de l’application (AppHeader)
**Fichier : `components/AppHeader.js`**
```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function AppHeader() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>My Restaurant</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#F4CE14',
    paddingTop: 50,
    paddingBottom: 16,
  },
  title: {
    textAlign: 'center',
    fontSize: 28,
    fontWeight: 'bold',
    color: 'black',
  },
});
```

---

## 5. Étape 4 : Créer le pied de page (AppFooter)
**Fichier : `components/AppFooter.js`**
```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function AppFooter() {
  return (
    <View style={styles.container}>
      <Text style={styles.footerText}>
        All rights reserved by My Restaurant, 2025
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#EE9972',
    paddingVertical: 10,
  },
  footerText: {
    textAlign: 'center',
    fontSize: 14,
    fontStyle: 'italic',
    color: '#333333',
  },
});
```

---

## 6. Étape 5 : Définir les données du menu et la SectionList (MenuItems – partie 1)
**Fichier : `components/MenuItems.js`**
```javascript
import React from 'react';
import { View, Text, StyleSheet, SectionList } from 'react-native';

const menuItemsToDisplay = [
  {
    title: 'Appetizers',
    data: [
      { name: 'Hummus', price: '$5.00' },
      { name: 'Moutabal', price: '$5.00' },
      { name: 'Falafel', price: '$7.50' },
      { name: 'Marinated Olives', price: '$5.00' },
      { name: 'Kofta', price: '$5.00' },
      { name: 'Eggplant Salad', price: '$8.50' },
    ],
  },
  {
    title: 'Main Dishes',
    data: [
      { name: 'Lentil Burger', price: '$10.00' },
      { name: 'Smoked Salmon', price: '$14.00' },
      { name: 'Kofta Burger', price: '$11.00' },
      { name: 'Turkish Kebab', price: '$15.50' },
    ],
  },
  {
    title: 'Sides',
    data: [
      { name: 'Fries', price: '$3.00' },
      { name: 'Buttered Rice', price: '$3.00' },
      { name: 'Bread Sticks', price: '$3.00' },
      { name: 'Pita Pocket', price: '$3.00' },
      { name: 'Lentil Soup', price: '$3.75' },
      { name: 'Greek Salad', price: '$6.00' },
      { name: 'Rice Pilaf', price: '$4.00' },
    ],
  },
  {
    title: 'Desserts',
    data: [
      { name: 'Baklava', price: '$3.00' },
      { name: 'Tartufo', price: '$3.00' },
      { name: 'Tiramisu', price: '$5.00' },
      { name: 'Panna Cotta', price: '$5.00' },
    ],
  },
];
```

---

## 7. Étape 6 : Créer le composant Item pour une ligne du menu
```javascript
const Item = ({ name, price }) => (
  <View style={styles.itemRow}>
    <Text style={styles.itemText}>{name}</Text>
    <Text style={styles.itemPrice}>{price}</Text>
  </View>
);
```

---

## 8. Étape 7 : Configurer SectionList (renderItem + renderSectionHeader)
```javascript
export default function MenuItems() {
  const renderItem = ({ item }) => (
    <Item name={item.name} price={item.price} />
  );

  const renderSectionHeader = ({ section: { title } }) => (
    <Text style={styles.sectionHeader}>{title}</Text>
  );

  return (
    <View style={styles.container}>
      <SectionList
        sections={menuItemsToDisplay}
        keyExtractor={(item, index) => item.name + index}
        renderItem={renderItem}
        renderSectionHeader={renderSectionHeader}
      />
    </View>
  );
}
```

---

## 9. Étape 8 : Ajouter un séparateur et un pied de page SectionList
```javascript
const Separator = () => <View style={styles.separator} />;

const ListFooter = () => (
  <Text style={styles.listFooterText}>
    All rights reserved by My Restaurant, 2025
  </Text>
);

// Dans SectionList :
ItemSeparatorComponent={Separator}
ListFooterComponent={ListFooter}
```

---

## 10. Étape 9 : Ajouter les styles complets
```javascript
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#333333',
  },
  sectionHeader: {
    backgroundColor: '#F4CE14',
    color: 'black',
    fontSize: 22,
    fontWeight: 'bold',
    textAlign: 'center',
    paddingVertical: 8,
  },
  itemRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingHorizontal: 24,
    paddingVertical: 12,
    backgroundColor: '#333333',
  },
  itemText: {
    color: '#EDEFEE',
    fontSize: 18,
  },
  itemPrice: {
    color: '#EDEFEE',
    fontSize: 18,
  },
  separator: {
    borderBottomWidth: 1,
    borderColor: '#EDEFEE',
  },
  listFooterText: {
    paddingVertical: 10,
    textAlign: 'center',
    fontSize: 14,
    fontStyle: 'italic',
    color: '#EDEFEE',
    backgroundColor: '#333333',
  },
});
```

---

## 11. Étape 10 : Intégrer dans App.js
```javascript
import * as React from 'react';
import { View, StyleSheet, StatusBar } from 'react-native';

import AppHeader from './components/AppHeader';
import AppFooter from './components/AppFooter';
import MenuItems from './components/MenuItems';

export default function App() {
  return (
    <>
      <StatusBar barStyle="light-content" />
      <View style={styles.container}>
        <AppHeader />
        <MenuItems />
      </View>
      <View style={styles.footerContainer}>
        <AppFooter />
      </View>
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#333333',
  },
  footerContainer: {
    backgroundColor: '#333333',
  },
});
```
