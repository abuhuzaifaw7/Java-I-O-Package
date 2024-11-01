# Java-I-O-Package
The Java I/O package provides classes for input and output operations, including reading, writing, and managing data streams, files, and serialization.


The `java.io` package in Java provides the `File` class, which represents files and directories in a file system. The `File` class offers a way to access and manipulate file and directory attributes, including creating, deleting, checking existence, and obtaining file properties. This class does not perform actual reading or writing of file contents (which is done by `FileReader`, `FileWriter`, `FileInputStream`, and `FileOutputStream`), but it’s essential for managing files and directories.

### 1. **Creating a File Object**
A `File` object represents a path in the filesystem, either as an absolute or relative path. Here’s how to create a `File` object in Java:
```java
import java.io.File;

public class FileExample {
    public static void main(String[] args) {
        File file = new File("example.txt"); // Creates a File object for a file named "example.txt"
    }
}
```

### 2. **Commonly Used Methods of the `File` Class**

#### 1. **Checking File or Directory Existence**
   - `boolean exists()`: Returns `true` if the file or directory exists.
   - `boolean isFile()`: Returns `true` if the path points to a file.
   - `boolean isDirectory()`: Returns `true` if the path points to a directory.
   
   **Example**:
   ```java
   File file = new File("example.txt");
   System.out.println("Exists: " + file.exists());
   System.out.println("Is File: " + file.isFile());
   System.out.println("Is Directory: " + file.isDirectory());
   ```

#### 2. **Creating Files and Directories**
   - `boolean createNewFile()`: Creates a new file. Returns `true` if the file was created successfully.
   - `boolean mkdir()`: Creates a single directory. Returns `true` if the directory was created successfully.
   - `boolean mkdirs()`: Creates the directory and any necessary parent directories.

   **Example**:
   ```java
   File newFile = new File("newfile.txt");
   File newDir = new File("newdir");

   try {
       boolean fileCreated = newFile.createNewFile();
       System.out.println("File Created: " + fileCreated);
   } catch (IOException e) {
       e.printStackTrace();
   }

   boolean dirCreated = newDir.mkdir();
   System.out.println("Directory Created: " + dirCreated);
   ```

#### 3. **Getting File Information**
   - `String getName()`: Returns the name of the file or directory.
   - `String getPath()`: Returns the path (relative or absolute) to the file.
   - `String getAbsolutePath()`: Returns the absolute path of the file.
   - `long length()`: Returns the length (in bytes) of the file.
   - `long lastModified()`: Returns the last modified time in milliseconds since the epoch (January 1, 1970).
   
   **Example**:
   ```java
   File file = new File("example.txt");

   System.out.println("File Name: " + file.getName());
   System.out.println("File Path: " + file.getPath());
   System.out.println("Absolute Path: " + file.getAbsolutePath());
   System.out.println("File Size: " + file.length() + " bytes");
   System.out.println("Last Modified: " + file.lastModified());
   ```

#### 4. **File Permissions**
   - `boolean canRead()`: Returns `true` if the file is readable.
   - `boolean canWrite()`: Returns `true` if the file is writable.
   - `boolean canExecute()`: Returns `true` if the file is executable.
   - `boolean setReadOnly()`: Sets the file to read-only. Returns `true` if successful.
   - `boolean setWritable(boolean writable)`: Sets the write permission.
   - `boolean setReadable(boolean readable)`: Sets the read permission.
   
   **Example**:
   ```java
   File file = new File("example.txt");

   System.out.println("Can Read: " + file.canRead());
   System.out.println("Can Write: " + file.canWrite());
   System.out.println("Can Execute: " + file.canExecute());

   file.setReadOnly();
   System.out.println("Set to Read Only. Can Write: " + file.canWrite());
   ```

#### 5. **Listing Files in a Directory**
   - `String[] list()`: Returns an array of file names in the directory.
   - `File[] listFiles()`: Returns an array of `File` objects representing files in the directory.
   
   **Example**:
   ```java
   File directory = new File("testdir");

   String[] fileList = directory.list();
   System.out.println("Files in directory:");
   for (String name : fileList) {
       System.out.println(name);
   }

   File[] files = directory.listFiles();
   System.out.println("Files and directories:");
   for (File f : files) {
       System.out.println(f.getName() + (f.isDirectory() ? " (Directory)" : " (File)"));
   }
   ```

#### 6. **Deleting Files and Directories**
   - `boolean delete()`: Deletes the file or directory. If it’s a directory, it must be empty to delete successfully.

   **Example**:
   ```java
   File fileToDelete = new File("delete_me.txt");
   boolean deleted = fileToDelete.delete();
   System.out.println("File Deleted: " + deleted);
   ```

#### 7. **Renaming and Moving Files**
   - `boolean renameTo(File dest)`: Renames or moves the file to the specified destination.

   **Example**:
   ```java
   File oldFile = new File("oldfile.txt");
   File newFile = new File("newfile.txt");

   boolean renamed = oldFile.renameTo(newFile);
   System.out.println("File Renamed: " + renamed);
   ```

---

### Example Program Using File Class Methods
The following example demonstrates how to create a file, check its properties, and then delete it.
```java
import java.io.File;
import java.io.IOException;

public class FileClassDemo {
    public static void main(String[] args) {
        File file = new File("example.txt");

        // Create a new file
        try {
            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists.");
            }
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }

        // Get file information
        System.out.println("File Name: " + file.getName());
        System.out.println("File Path: " + file.getPath());
        System.out.println("Absolute Path: " + file.getAbsolutePath());
        System.out.println("File Size: " + file.length() + " bytes");
        System.out.println("Last Modified: " + file.lastModified());

        // Check permissions
        System.out.println("Can Read: " + file.canRead());
        System.out.println("Can Write: " + file.canWrite());
        System.out.println("Can Execute: " + file.canExecute());

        // Delete the file
        if (file.delete()) {
            System.out.println("File deleted successfully.");
        } else {
            System.out.println("Failed to delete the file.");
        }
    }
}
```

### Summary of Key Methods

| Method                  | Description                                      |
|-------------------------|--------------------------------------------------|
| `exists()`              | Checks if file or directory exists               |
| `isFile()`              | Checks if path is a file                         |
| `isDirectory()`         | Checks if path is a directory                    |
| `createNewFile()`       | Creates a new file                               |
| `mkdir()`, `mkdirs()`   | Creates a new directory (or directories)         |
| `delete()`              | Deletes the file or directory                    |
| `getName()`, `getPath()`| Retrieves file name and path                     |
| `length()`              | Returns file size                                |
| `canRead()`, `canWrite()` | Checks read/write permissions                  |
| `renameTo(File dest)`   | Renames or moves the file                        |


<br><br>
## 2. **File Class Methods in Java**
<br>
The `File` class is an essential part of file management in Java, allowing developers to easily interact with and manage files and directories within the file system.


In Java, the `File` class in the `java.io` package provides several useful methods for working with files and directories. Here’s a list of commonly used `File` class methods for file and directory operations, specifically for listing files:

### 1. `list()`
- **Description**: Returns an array of strings representing the names of the files and directories in the specified directory.
- **Usage**:
  ```java
  File directory = new File("path/to/directory");
  String[] files = directory.list();
  if (files != null) {
      for (String fileName : files) {
          System.out.println(fileName);
      }
  }
  ```

### 2. `listFiles()`
- **Description**: Returns an array of `File` objects representing the files and directories in the specified directory.
- **Usage**:
  ```java
  File directory = new File("path/to/directory");
  File[] files = directory.listFiles();
  if (files != null) {
      for (File file : files) {
          System.out.println(file.getName());
      }
  }
  ```

### 3. `list(FilenameFilter filter)`
- **Description**: Returns an array of strings of the names of files and directories that satisfy the specified filter.
- **Usage**:
  ```java
  File directory = new File("path/to/directory");
  String[] files = directory.list((dir, name) -> name.endsWith(".txt"));
  if (files != null) {
      for (String fileName : files) {
          System.out.println(fileName);
      }
  }
  ```

### 4. `listFiles(FilenameFilter filter)`
- **Description**: Returns an array of `File` objects of the files and directories in the directory that satisfy the specified filter.
- **Usage**:
  ```java
  File directory = new File("path/to/directory");
  File[] files = directory.listFiles((dir, name) -> name.endsWith(".txt"));
  if (files != null) {
      for (File file : files) {
          System.out.println(file.getName());
      }
  }
  ```

### 5. `listFiles(FileFilter filter)`
- **Description**: Returns an array of `File` objects representing files and directories that match a given `FileFilter`.
- **Usage**:
  ```java
  File directory = new File("path/to/directory");
  File[] files = directory.listFiles(file -> file.isFile() && file.getName().endsWith(".txt"));
  if (files != null) {
      for (File file : files) {
          System.out.println(file.getName());
      }
  }
  ```

These methods are essential for file and directory management in Java, allowing you to filter files based on custom conditions, making file handling more flexible and efficient.
