# UNIT-TEST_5
***Другие виды тестирования***

***Задание №1:***
***Представьте, что вы работаете над разработкой простого приложения для записной книжки,
которое позволяет пользователям добавлять, редактировать и удалять контакты.
Ваша задача - придумать как можно больше различных тестов (юнит-тесты, интеграционные тесты,
сквозные тесты) для этого приложения. Напишите название каждого теста, его тип и краткое описание того,
что этот тест проверяет?***

testAddContact(Unit): // проверяет возможность добавления нового контакта в записную книжку

@Test
public void testAddContact() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание нового контакта
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    
    // Добавление контакта в записную книжку
    addressBook.addContact(contact);
    
    // Проверка, что контакт добавлен
    assertTrue(addressBook.containsContact(contact));
}


testEditContact(Unit): // проверяет возможность редактирования контакта в записной книжке

@Test
public void testEditContact() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание и добавление контакта в записную книжку
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    addressBook.addContact(contact);
    
    // Создание новых данных для контакта
    Contact newContactData = new Contact("Jane", "Smith", "jane.smith@example.com");
    
    // Редактирование контакта
    addressBook.editContact(contact, newContactData);
    
    // Проверка, что контакт был успешно отредактирован
    assertEquals(newContactData, contact);
}


testDeleteContact(Unit): // проверяет возможность удаления контакта из записной книжки

@Test
public void testDeleteContact() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание и добавление контакта в записную книжку
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    addressBook.addContact(contact);
    
    // Удаление контакта
    addressBook.deleteContact(contact);
    
    // Проверка, что контакт был успешно удален
    assertFalse(addressBook.containsContact(contact));
}


testAddContactIntegration(Integration): // проверяет интеграцию функции добавления контакта с другими компонентами приложения

@Test
public void testAddContactIntegration() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание нового контакта
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    
    // Добавление контакта в записную книжку
    addressBook.addContact(contact);
    
    // Проверка, что контакт успешно добавлен и отображается в пользовательском интерфейсе
    assertTrue(addressBook.containsContact(contact));
    assertTrue(addressBookUI.isContactDisplayed(contact));
}


testEditContactIntegration(Integration): // проверяет интеграцию функции редактирования контакта с другими компонентами 				// приложения

@Test
public void testEditContactIntegration() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание и добавление контакта в записную книжку
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    addressBook.addContact(contact);
    
    // Создание новых данных для контакта
    Contact newContactData = new Contact("Jane", "Smith", "jane.smith@example.com");
    
    // Редактирование контакта
    addressBook.editContact(contact, newContactData);
    
    // Проверка, что контакт был успешно отредактирован и изменения отображаются в пользовательском интерфейсе
    assertEquals(newContactData, contact);
    assertTrue(addressBookUI.isContactDisplayed(newContactData));
}


testDeleteContactIntegration(Integration): // проверяет интеграцию функции удаления контакта с другими компонентами приложения

@Test
public void testDeleteContactIntegration() {
    // Создание экземпляра записной книжки

AddressBook addressBook = new AddressBook();
// Создание и добавление контакта в записную книжку

Contact contact = new Contact("John", "Doe", "john.doe@example.com");
addressBook.addContact(contact);

// Удаление контакта
addressBook.deleteContact(contact);

// Проверка, что контакт успешно удален и отсутствует в пользовательском интерфейсе
assertFalse(addressBook.containsContact(contact));
assertFalse(addressBookUI.isContactDisplayed(contact));
}


testSaveContactsToFile(Unit): // проверяет возможность сохранения контактов в файл

@Test
public void testSaveContactsToFile() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание и добавление контактов в записную книжку
    Contact contact1 = new Contact("John", "Doe", "john.doe@example.com");
    Contact contact2 = new Contact("Jane", "Smith", "jane.smith@example.com");
    addressBook.addContact(contact1);
    addressBook.addContact(contact2);
    
    // Указание пути к файлу
    String filePath = "contacts.txt";
    
    // Сохранение контактов в файл
    addressBook.saveContactsToFile(filePath);
    
    // Проверка, что файл успешно создан и содержит данные контактов
    assertTrue(fileExists(filePath));
    assertEquals(fileContents(filePath), "John Doe john.doe@example.com\nJane Smith jane.smith@example.com");
}


testLoadContactsFromFile(Unit): // проверяет возможность загрузки контактов из файла

@Test
public void testLoadContactsFromFile() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Указание пути к существующему файлу с данными контактов
    String filePath = "contacts.txt";
    
    // Загрузка контактов из файла
    addressBook.loadContactsFromFile(filePath);
    
    // Проверка, что контакты были успешно загружены
    assertTrue(addressBook.containsContact(new Contact("John", "Doe", "john.doe@example.com")));
    assertTrue(addressBook.containsContact(new Contact("Jane", "Smith", "jane.smith@example.com")));
}


testSearchContact(Unit): // проверяет возможность поиска контакта по имени или электронной почте

@Test
public void testSearchContact() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание и добавление контактов в записную книжку
    Contact contact1 = new Contact("John", "Doe", "john.doe@example.com");
    Contact contact2 = new Contact("Jane", "Smith", "jane.smith@example.com");
    addressBook.addContact(contact1);
    addressBook.addContact(contact2);
    
    // Поиск контакта по имени "John"
    Contact foundContact1 = addressBook.searchContact("John");
    
    // Поиск контакта по электронной почте "jane.smith@example.com"
    Contact foundContact2 = addressBook.searchContact("jane.smith@example.com");
    
    // Проверка, что контакты были успешно найдены
    assertEquals(contact1, foundContact1);
    assertEquals(contact2, foundContact2);
}


***Задание №2:***
***Ниже список тестовых сценариев. Ваша задача - определить тип каждого теста (юнит-тест,
интеграционный тест, сквозной тест) и объяснить, почему вы так решили.
Проверка того, что функция addContact корректно добавляет новый контакт в список контактов".
"Проверка того, что при добавлении контакта через пользовательский интерфейс, контакт корректно
отображается в списке контактов".
"Проверка полного цикла работы с контактом: создание контакта, его редактирование и
последующее удаление".***


Тип теста: Юнит-тест.

@Test
public void testAddContact() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание нового контакта
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    
    // Добавление контакта в записную книжку
    addressBook.addContact(contact);
    
    // Проверка, что контакт добавлен
    assertTrue(addressBook.containsContact(contact));
}


Тип теста: Интеграционный тест.

@Test
public void testAddContactIntegration() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание нового контакта
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    
    // Добавление контакта через пользовательский интерфейс
    addressBookUI.addContact(contact);
    
    // Проверка, что контакт успешно добавлен и отображается в пользовательском интерфейсе
    assertTrue(addressBook.containsContact(contact));
    assertTrue(addressBookUI.isContactDisplayed(contact));
}


Тип теста: Сквозной тест.

@Test
public void testCreateEditDeleteContact() {
    // Создание экземпляра записной книжки
    AddressBook addressBook = new AddressBook();
    
    // Создание нового контакта
    Contact contact = new Contact("John", "Doe", "john.doe@example.com");
    
    // Добавление контакта в записную книжку
    addressBook.addContact(contact);
    
    // Редактирование контакта
    Contact newContactData = new Contact("Jane", "Smith", "jane.smith@example.com");
    addressBook.editContact(contact, newContactData);
    
    // Проверка, что контакт был успешно отредактирован
    assertEquals(newContactData, contact);
    
    // Удаление контакта
    addressBook.deleteContact(contact);
    
    // Проверка, что контакт был успешно удален
    assertFalse(addressBook.containsContact(contact));
}
