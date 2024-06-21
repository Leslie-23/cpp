Creating a GUI application in C++ can be done using various libraries, but one of the most popular and widely-used libraries is Qt. Qt is a powerful toolkit for creating cross-platform applications with rich user interfaces.

Here, I'll provide an example of a simple Qt application that takes user input and stores it. This example assumes you have Qt installed and set up on your development environment.

### Step 1: Install Qt

If you haven't already, download and install Qt from [Qt's official website](https://www.qt.io/download).

### Step 2: Create a New Qt Project

Use Qt Creator to create a new Qt Widgets Application. Name it `UserInfoApp`.

### Step 3: Modify `UserInfoApp.pro` File

Ensure your `.pro` file includes the necessary modules:

```plaintext
QT += core gui

greaterThan(QT_MAJOR_VERSION, 4): QT += widgets

TARGET = UserInfoApp
TEMPLATE = app

SOURCES += main.cpp \
           mainwindow.cpp

HEADERS += mainwindow.h

FORMS += mainwindow.ui
```

### Step 4: Create the UI in Qt Designer

Open `mainwindow.ui` in Qt Designer and add the following widgets:
- Two `QLineEdit` widgets for user input (e.g., `nameLineEdit` and `ageLineEdit`).
- One `QPushButton` widget for submission (e.g., `submitButton`).
- One `QTextEdit` widget to display stored information (e.g., `infoTextEdit`).

### Step 5: Modify `mainwindow.h`

Define the slots and UI elements in the header file:

```cpp
#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QStringList>

QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();

private slots:
    void on_submitButton_clicked();

private:
    Ui::MainWindow *ui;
    QStringList userInfoList;
};

#endif // MAINWINDOW_H
```

### Step 6: Implement the Logic in `mainwindow.cpp`

Add the logic for handling user input and storing/displaying it:

```cpp
#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
}

MainWindow::~MainWindow()
{
    delete ui;
}

void MainWindow::on_submitButton_clicked()
{
    QString name = ui->nameLineEdit->text();
    QString age = ui->ageLineEdit->text();

    if (!name.isEmpty() && !age.isEmpty()) {
        QString userInfo = QString("Name: %1, Age: %2").arg(name).arg(age);
        userInfoList.append(userInfo);

        ui->infoTextEdit->clear();
        for (const QString &info : userInfoList) {
            ui->infoTextEdit->append(info);
        }

        ui->nameLineEdit->clear();
        ui->ageLineEdit->clear();
    }
}
```

### Step 7: Main Application Entry Point (`main.cpp`)

Ensure your `main.cpp` is set up to launch the application:

```cpp
#include "mainwindow.h"

#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    MainWindow w;
    w.show();
    return a.exec();
}
```

### Step 8: Build and Run the Application

1. Open Qt Creator.
2. Load the project by opening the `UserInfoApp.pro` file.
3. Build and run the project.

### Explanation

1. **UI Setup**: The `mainwindow.ui` file is used to design the GUI using Qt Designer. It includes input fields (`QLineEdit`), a submit button (`QPushButton`), and a text area to display stored information (`QTextEdit`).
   
2. **Event Handling**: The `on_submitButton_clicked` slot is connected to the submit button's `clicked` signal. When the button is clicked, the slot retrieves the text from the input fields, appends the information to a list, and updates the text area to display all stored information.

3. **Data Storage**: The `QStringList` `userInfoList` is used to store the user input. This list is displayed in the `QTextEdit` widget.

By following these steps, you can create a simple Qt application in C++ that takes user input, stores it, and displays it in the application window. For more advanced features and customizations, refer to the [Qt documentation](https://doc.qt.io/).
