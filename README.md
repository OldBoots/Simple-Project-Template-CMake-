# Simple Project Template (CMake)

This is a convenient project template with a simple C structure.
The project contains:
- CMakeLists.txt
- .gitignore
- .clang-format
- LICENSE
- README\.md

## Project Structure:
```
project/
├── src/
│ ├── CMakeLists.txt
│ ├── main.c
│ └── module/
│ ├── hello.c
│ └── hello.h
├── CMakeLists.txt
├── LICENSE
├── README.md
├── .clang-format
└── .gitignore
```

## Build and Management:
> All commands are executed from the project root
### Build:
    mkdir build
    cmake -S . -B build                             # Generate MakeFiles
    cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug    # Generate MakeFiles with debug info
    cmake -S . -B build -DCMAKE_BUILD_TYPE=Release  # Generate MakeFiles without debug info

    cmake --build build # Build the project
    or
    make -C build       # Build the project

### Project Management:
    cmake --build build --target check-format   # Check code style (NoBuild)
    cmake --build build --target fix-format     # Fix code style (NoBuild)
    cmake --build build --target build-format   # Fix code style and build the project
    cmake --build build --target clean          # Clean object files
    cmake --build build --target clean-all      # Completely clean the build directory
    or
    make -C build check-format  # Check code style (NoBuild)
    make -C build fix-format    # Fix code style (NoBuild)
    make -C build build-format  # Fix code style and build the project
    make -C build clean         # Clean object files
    make -C build clean-all     # Completely clean the build directory




# Шаблон простого пректа (CMake)

Это удобный шаблон проекта с простой структурой на C. 
Проект содержит:
- CMakeLists.txt
- .gitignore
- .clang-formft
- LICENZE
- README\.md

## Структра проекта:
```
project/
├── src/
│ ├── CMakeLists.txt
│ ├── main.c
│ └── module/
│ ├── hello.c
│ └── hello.h
├── CMakeLists.txt
├── LICENSE
├── README.md
├── .clang-format
└── .gitignore
```
## Сборка и управление:
> Все команды выполняются в корне проекта

### Сборка:
    mkdir build
    cmake -S . -B build                             # Сборка MakeFiles
    cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug    # Сборка MakeFiles с debug-информацие
    cmake -S . -B build -DCMAKE_BUILD_TYPE=Release  # Сборка MakeFiles без debug-информации

    cmake --build build # Сборка проекта
    или
    make -C build       # Сборка проекта

### Управление проектом:
    cmake --build build --target check-format   # Проверяет кодстайл (NoBuild)
    cmake --build build --target fix-format     # Исправляет кодстайл (NoBuild)
    cmake --build build --target build-format   # Исправляет кодстайл и собирает проект
    cmake --build build --target clean          # Отчищает объектные файлы
    cmake --build build --target clean-all      # Полность отчищает директорию build
    или
    make -C build check-format  # Проверяет кодстайл (NoBuild)
    make -C build fix-format    # Исправляет кодстайл (NoBuild)
    make -C build build-format  # Исправляет кодстайл и собирает проект
    make -C build clean         # Отчищает объектные файлы
    make -C build clean-all     # Полность отчищает директорию build
