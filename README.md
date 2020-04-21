# javafx-jdbc
# Welcome to my JavaFX with JDBC project
## Main goal:
1. Introduce the student to the development of JavaFX applications with JDBC
1. Allow the student to know the fundamentals and the use of the tools, so that he can
then continue studying, in a comfortable way, the specifics you want
- [x] REQUIREMENTS: OO & Lambda & JDBC & JavaFX

## Local project created
- Checklist:
- [x] User libraries: JavaFX, MySQLConnector
- [x] Run configurarions -> VM arguments:
--module-path C:\java-libs\javafx-sdk\lib --add-modules=javafx.fxml,javafx.controls

## Main view
- Checklist:
- [x] Create FXML "MainView" (package "gui")
- [x] Load FXML in Main
- [x] Update Main.java
~~~java
	@Override
	public void start(Stage primaryStage) {
		try {
			FXMLLoader loader = new FXMLLoader(getClass().getResource("/gui/MainView.fxml"));
			Parent parent = loader.load();
			Scene mainScene = new Scene(parent);
			primaryStage.setScene(mainScene);
			primaryStage.setTitle("Sample JavaFX application");
			primaryStage.show();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
~~~


## Main view design
- Checklist:
- [x] Design MainView.fxml
- [x] Customize menu items
- [x] Update Main.java
~~~XML
<?xml version="1.0" encoding="UTF-8"?>
<?import javafx.scene.control.Menu?>
<?import javafx.scene.control.MenuBar?>
<?import javafx.scene.control.MenuItem?>
<?import javafx.scene.control.ScrollPane?>
<?import javafx.scene.layout.VBox?>
<ScrollPane maxHeight="-Infinity" maxWidth="-Infinity"
	minHeight="-Infinity" minWidth="-Infinity" prefHeight="400.0"
	prefWidth="600.0" xmlns="http://javafx.com/javafx/10.0.1"
	xmlns:fx="http://javafx.com/fxml/1">
	<content>
		<VBox prefHeight="326.0" prefWidth="513.0">
			<children>
				<MenuBar>
					<menus>
						<Menu mnemonicParsing="false" text="Registration">
							<items>
								<MenuItem mnemonicParsing="false" text="Seller" />
								<MenuItem mnemonicParsing="false" text="Departments" />
							</items>
						</Menu>
						<Menu mnemonicParsing="false" text="Help">
							<items>
								<MenuItem mnemonicParsing="false" text="About" />
							</items>
						</Menu>
					</menus>
				</MenuBar>
			</children>
		</VBox>
	</content>
</ScrollPane>
~~~

## Main view controller
- Checklist:
- [x] Create controller
- [x] In view, associate controller, ids, events

## About view
- Checklist:
- [x]  Include util classes to the project (Alerts.java, Constraints.java)
https://github.com/acenelio/javafx5/blob/master/src/gui/util/Alerts.java
https://github.com/acenelio/javafx5/blob/master/src/gui/util/Constraints.java
- [x] Create About.fxml (VBox)
- [x] In Main.java, expose mainScene reference
- [x] In MainViewController.java, create loadView method

## DepartmentList view design
- Checklist:
- [x] Create DepartmentList.fxml (VBox)
- [x] In MainViewController.java, load DepartmentList
~~~XML
<?xml version="1.0" encoding="UTF-8"?>
<?import javafx.geometry.Insets?>
<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.control.TableColumn?>
<?import javafx.scene.control.TableView?>
<?import javafx.scene.control.ToolBar?>
<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Font?>
<VBox maxHeight="-Infinity" maxWidth="-Infinity"
	minHeight="-Infinity" minWidth="-Infinity" prefHeight="400.0"
	prefWidth="600.0" xmlns="http://javafx.com/javafx/10.0.1"
	xmlns:fx="http://javafx.com/fxml/1">
	<children>
		<Label text="Department Registration">
			<font>
				<Font name="System Bold" size="14.0" />
			</font>
			<padding>
				<Insets left="5.0" top="5.0" />
			</padding>
		</Label>
		<ToolBar prefHeight="40.0" prefWidth="200.0">
			<items>
				<Button fx:id="btNew" mnemonicParsing="false" text="New" />
			</items>
		</ToolBar>
		<TableView prefHeight="200.0" prefWidth="200.0">
			<columns>
				<TableColumn prefWidth="75.0" text="Id" />
				<TableColumn prefWidth="75.0" text="Name" />
			</columns>
		</TableView>
	</children>
</VBox>
~~~

## DepartmentList controller
- Checklist:
- [x] Create model.entities.Department.java
https://github.com/acenelio/demo-dao-jdbc/blob/master/src/model/entities/Department.java
- [x] Create DepartmentListController.java
- [x] In view, associate controller, ids, events

## DepartmentService
- Checklist:
- [x] Create model.services.DepartmentService.java with findAll method
- [x] In DepartmentListController:
1. Create DepartmentService dependency with set method
1. Create ObservableList<Department>
1. Create updateTableViewData method

## Initializing action as parameter
- Checklist:
- [x] Add a Consumer<T> parameter to loadView method
- [x] After loading view, call accept from the Consumer
- [x] Add a consumer instance on loadView calls

## Adding database access
- Prerequisites:
- [x] MySQL server installed and running
- [x] Database created and instantiated
- [x] Data access layer implemented (DAO pattern):
- Checklist:
- [x] Add model.entities.Seller.java
- [x] Add db.properties do project
- [x] Add data access packages to project:
1. db
1. model.dao
1. model.dao.impl
- [x] In DepartmentService, add DepartmentDao dependency with Factory call

## DepartmentForm (dialog) design
- Checklist:
- [x] Create gui.util.Utils.java with currentStage method
- [x] Create DepartmentForm.fxml (AnchorPane)
1. GridPane 3x3 (anchors: 20 top, 20 left)
1. Id text box: not editable
1. Label error: red
1. HBox (spacing: 5)
- [x] In DepartmentListController, create createDialogForm method
- [x] Call createDialogForm on "new" button action
~~~XML
<?xml version="1.0" encoding="UTF-8"?>
<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.control.TextField?>
<?import javafx.scene.layout.AnchorPane?>
<?import javafx.scene.layout.ColumnConstraints?>
<?import javafx.scene.layout.GridPane?>
<?import javafx.scene.layout.HBox?>
<?import javafx.scene.layout.RowConstraints?>
<AnchorPane prefHeight="139.0" prefWidth="532.0"
	xmlns="http://javafx.com/javafx/10.0.1"
	xmlns:fx="http://javafx.com/fxml/1">
	<children>
		<GridPane layoutX="33.0" layoutY="32.0" prefHeight="95.0"
			prefWidth="499.0" AnchorPane.leftAnchor="20.0"
			AnchorPane.topAnchor="20.0">
			<columnConstraints>
				<ColumnConstraints hgrow="SOMETIMES"
					maxWidth="161.0" minWidth="10.0" prefWidth="63.0" />
				<ColumnConstraints hgrow="SOMETIMES"
					maxWidth="270.0" minWidth="10.0" prefWidth="160.0" />
				<ColumnConstraints hgrow="SOMETIMES"
					maxWidth="245.0" minWidth="10.0" prefWidth="243.0" />
			</columnConstraints>
			<rowConstraints>
				<RowConstraints minHeight="10.0" prefHeight="30.0"
					vgrow="SOMETIMES" />
				<RowConstraints minHeight="10.0" prefHeight="30.0"
					vgrow="SOMETIMES" />
				<RowConstraints minHeight="10.0" prefHeight="30.0"
					vgrow="SOMETIMES" />
			</rowConstraints>
			<children>
				<Label text="Id" />
				<Label text="Name" GridPane.rowIndex="1" />
				<Label textFill="RED" GridPane.columnIndex="2"
					GridPane.rowIndex="1" />
				<TextField editable="false" GridPane.columnIndex="1" />
				<TextField GridPane.columnIndex="1" GridPane.rowIndex="1" />
				<HBox prefHeight="100.0" prefWidth="200.0" spacing="5.0"
					GridPane.columnIndex="1" GridPane.rowIndex="2">
					<children>
						<Button mnemonicParsing="false" text="Save" />
						<Button mnemonicParsing="false" text="Cancel" />
					</children>
				</HBox>
			</children>
		</GridPane>
	</children>
</AnchorPane>
~~~

## DepartmentFormController
- Checklist:
- [x] Create DepartmentFormController.java
- [x] In view, associate controller, ids, events

## Passing a Department object to DepartmentForm view
- Checklist:
- [x] In DepartmentFormController
1. Create a Department dependency with set method
1. Create updateFormData method
- [x] In DepartmentListController
1. Update onBtNewAction method
1. Update createDialogForm method

## Saving a new Department
- Checklist:
- [x] In Utils, implement tryParseToInt method
- [x] In DepartmentService, create saveOrUpdate method
- [x] In DepartmentFormController
1. Create a DepartmentService dependency with set method
1. Implement onBtSaveAction
1. Implement onBtCancelAction
- [x] In DepartmentListController, inject DepartmentService instance

## Observer design pattern to update tableview
- Checklist:
- [x] Create interface gui.listeners.DataChangeListener
- [x] In DepartmentFormController (subject)
1. Create List<DataChangeListener> dependency with subscribe method
1. Notify subscribers when needed
- [x] In DepartmentListController (observer)
1. Implement DataChangeListener interface
1. Subscribe for DepartmentFormController

## Validation exception
- Checklist:
- [x] Create model.exceptions.ValidationException
- [x] In DepartmentFormController
1. In getFormData method, implement verifications and throw ValidationException
1. Implement setErrorMessages method
1. In onBtSaveAction, catch ValidationException

## Update department
- References:
https://stackoverflow.com/questions/32282230/fxml-javafx-8-tableview-make-a-delete-button-in-each-row-anddelete-the-row-a
- Checklist:
- [x] In DepartmentListController
1. Create new attribute: TableColumn<Department, Department> tableColumnEDIT;
1. Create initEditButtons method
1. In updateTableViewData, call initEditButtons
- [x] In DepartmentList.fxml
1. Include new table column
1. Associate id
~~~java
	private void initEditButtons() {
		tableColumnEDIT.setCellValueFactory(param -> new ReadOnlyObjectWrapper<>(param.getValue()));
		tableColumnEDIT.setCellFactory(param -> new TableCell<Department, Department>() {
			private final Button button = new Button("edit");

			@Override
			protected void updateItem(Department obj, boolean empty) {
				super.updateItem(obj, empty);
				if (obj == null) {
					setGraphic(null);
					return;
				}
				setGraphic(button);
				button.setOnAction(
						event -> createDialogForm(obj, "/gui/DepartmentForm.fxml", Utils.currentStage(event)));
			}
		});
	}
~~~ 

## Remove department
- References:
https://stackoverflow.com/questions/32282230/fxml-javafx-8-tableview-make-a-delete-button-in-each-row-anddelete-the-row-a
- Checklist:
- [x] In Alerts, create showConfirmation method
- [x] In DepartmentService, create remove method
- [x] In DepartmentListController
1. Create new attribute: TableColumn<Department, Department> tableColumnREMOVE;
1. Create initRemoveButtons method
- [x] Catch DbIntegrityException
1. In updateTableViewData, call initRemoveButtons
- [x] In DepartmentList.fxml
1. Include new table column
1. Associate id
~~~java
	public static Optional<ButtonType> showConfirmation(String title, String content) {
		Alert alert = new Alert(AlertType.CONFIRMATION);
		alert.setTitle(title);
		alert.setHeaderText(null);
		alert.setContentText(content);
		return alert.showAndWait();
	}

	private void initRemoveButtons() {
		tableColumnREMOVE.setCellValueFactory(param -> new ReadOnlyObjectWrapper<>(param.getValue()));
		tableColumnREMOVE.setCellFactory(param -> new TableCell<Department, Department>() {
			private final Button button = new Button("remove");

			@Override
			protected void updateItem(Department obj, boolean empty) {
				super.updateItem(obj, empty);
				if (obj == null) {
					setGraphic(null);
					return;
				}
				setGraphic(button);
				button.setOnAction(event -> removeEntity(obj));
			}
		});
	}
~~~

## Deleting .settings folder
- Checklist:
- [x] .gitignore: .settings/
- [x] Delete .settings/ folder

## SellerList
- Checklist:
- [x] Clone SellerService
1. Replace: Department -> Seller
- [x] Clone SellerListController
1. Replace: Department -> Seller
1. Comment createDialogForm
- [x] Clone SellerList.fxml
- [x] Replace: Department -> Seller
- [x] Update MainViewController.onMenuItemSellerAction

## Seller TableView
- References:
https://stackoverflow.com/questions/47484280/format-of-date-in-the-javafx-tableview
Checklist:
- [x] gui.utils.Util.java
1. formatTableColumnDate method
1. formatTableColumnDouble method
- [x] SellerListController
1. TableColumn attributes (Email, BirthDate, BaseSalary)
1. Update initializeNodes
- [x] SellerListView
1. TableColumn (Email, BirthDate, BaseSalary)
1. Associate fx:id
~~~java
	public static <T> void formatTableColumnDate(TableColumn<T, Date> tableColumn, String format) {
		tableColumn.setCellFactory(column -> {
			TableCell<T, Date> cell = new TableCell<T, Date>() {
				private SimpleDateFormat sdf = new SimpleDateFormat(format);

				@Override
				protected void updateItem(Date item, boolean empty) {
					super.updateItem(item, empty);
					if (empty) {
						setText(null);
					} else {
						setText(sdf.format(item));
					}
				}
			};
			return cell;
		});
	}

	public static <T> void formatTableColumnDouble(TableColumn<T, Double> tableColumn, int decimalPlaces) {
		tableColumn.setCellFactory(column -> {
			TableCell<T, Double> cell = new TableCell<T, Double>() {
				@Override
				protected void updateItem(Double item, boolean empty) {
					super.updateItem(item, empty);
					if (empty) {
						setText(null);
					} else {
						Locale.setDefault(Locale.US);
						setText(String.format("%." + decimalPlaces + "f", item));
					}
				}
			};
			return cell;
		});
	}
~~~

## SellerForm
- Checklist:
- [x] Clone SellerFormController
1. Replace: Department -> Seller
- [x] Clone SellerForm view
1. Replace: Department -> Seller
- [x] SellerListController
1. Uncomment createDialogForm

## TextField & DatePicker
- References:
https://stackoverflow.com/questions/26831978/javafx-datepicker-getvalue-in-a-specific-format
- Checklist:
- [x] gui.utils.Util.java
1. formatDatePicker method
- [x] TextField & DatePicker attributes (Email, BirthDate, BaseSalary)
- [x] Label error attributes (Email, BirthDate, BaseSalary)
- [x] Edit SellerFormView
- [x] Bugfix: SellerDaoJDBC.instantiateSeller
obj.setBirthDate(new java.util.Date(rs.getTimestamp("BirthDate").getTime()));
- [x] Update: initializeNodes
- [x] Update: updateFormData

~~~java
	public static void formatDatePicker(DatePicker datePicker, String format) {
		datePicker.setConverter(new StringConverter<LocalDate>() {
			DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern(format);
			{
				datePicker.setPromptText(format.toLowerCase());
			}

			@Override
			public String toString(LocalDate date) {
				if (date != null) {
					return dateFormatter.format(date);
				} else {
					return "";
				}
			}

			@Override
			public LocalDate fromString(String string) {
				if (string != null && !string.isEmpty()) {
					return LocalDate.parse(string, dateFormatter);
				} else {
					return null;
				}
			}
		});
	}
~~~

## Department ComboBox
- Checklist:
- [x] Update controller:
1. DepartmentService dependency
- [x] attribute
- [x] set method
1. ComboBox<Department> comboBoxDepartment
1. ObservableList<Department> obsList
- [x] loadAssociatedObjects
1. initializeComboBoxDepartment
1. updateFormData
- [x] Update view:
1. ComboBox
1. fx:id

~~~java
	private void initializeComboBoxDepartment() {
		Callback<ListView<Department>, ListCell<Department>> factory = lv -> new ListCell<Department>() {
			@Override
			protected void updateItem(Department item, boolean empty) {
				super.updateItem(item, empty);
				setText(empty ? "" : item.getName());
			}
		};
		comboBoxDepartment.setCellFactory(factory);
		comboBoxDepartment.setButtonCell(factory.call(null));
	}
~~~

## Saving Seller
- Checklist:
- [x] Update: getFormData
- [x] Update: setErrorMessages

## Building JAR file
- Checklist:
- [x] Build JAR file
1. Right click project name -> Export -> Java/Runnable JAR file -> Next
1. Select Main class
1. Select destination folder
1. Library handling: 3rd option
- [x] Pack files
1. JAR file
1. db.properties
1. MySQL Connector
1. JavaFX SDK
1. Java SDK
