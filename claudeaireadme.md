# Eve Processing Library

A Processing library template for creating visual programming extensions. This project provides scaffolding and best practices for developing Processing libraries, including example classes, build configuration, and automated release workflows.

## Project Structure

```
eve-processing/
├── src/main/java/com/myDomain/myLibrary/   # Library source code
│   ├── Grid.java                            # Visual grid with pulsing dots
│   └── Palette.java                         # Color palette generator
├── examples/HelloCircles/                   # Example Processing sketch
├── docs/                                    # Documentation (MkDocs)
├── .github/workflows/                       # CI/CD automation
├── build.gradle.kts                         # Gradle build configuration
└── release.properties                       # Library metadata
```

## Main Entry Points

### Grid.java

Creates a visual grid of animated pulsing dots. Located at `src/main/java/com/myDomain/myLibrary/Grid.java`.

**Constructor:**
```java
Grid(PApplet parent, int[] colors)
```
- `parent` - Reference to the Processing sketch
- `colors` - Array of colors for the dots

**Methods:**
```java
void show()  // Display and animate the grid
```

**Usage in Processing:**
```processing
import com.myDomain.myLibrary.*;

Grid grid;
Palette palette;

void setup() {
  size(500, 500);
  palette = new Palette(this);
  grid = new Grid(this, palette.getPalette());
}

void draw() {
  background(0);
  grid.show();
}
```

### Palette.java

Generates random color palettes using HSB color mode. Located at `src/main/java/com/myDomain/myLibrary/Palette.java`.

**Constructor:**
```java
Palette(PApplet parent)
```
- `parent` - Reference to the Processing sketch

**Methods:**
```java
int[] getPalette()  // Generate array of 5 random colors
```

**Usage in Processing:**
```processing
import com.myDomain.myLibrary.*;

Palette palette;

void setup() {
  size(400, 100);
  palette = new Palette(this);
  int[] colors = palette.getPalette();

  // Use colors for drawing
  for (int i = 0; i < colors.length; i++) {
    fill(colors[i]);
    rect(i * 80, 0, 80, 100);
  }
}
```

## Building the Library

### Prerequisites

- Java 17 or higher
- Gradle 8.5+ (included via wrapper)

### Build Commands

```bash
# Compile the library
./gradlew build

# Create JAR file
./gradlew jar

# Generate Javadoc
./gradlew javadoc

# Build complete release package
./gradlew buildReleaseArtifacts

# Deploy to local Processing sketchbook for testing
./gradlew deployToProcessingSketchbook
```

### Build Output

- `build/libs/` - Compiled JAR file
- `release/` - Complete release package (ZIP, PDEX, metadata)

## Development

### IDE Setup

The project supports:
- IntelliJ IDEA
- Visual Studio Code
- Eclipse

Open the project folder and import as a Gradle project.

### Adding Dependencies

Edit `build.gradle.kts` to add dependencies:

```kotlin
dependencies {
    compileOnly("org.processing:core:4.3.1")
    // Add your dependencies here
    implementation("your.dependency:artifact:version")
}
```

### Local Testing

1. Build the library: `./gradlew jar`
2. Deploy to sketchbook: `./gradlew deployToProcessingSketchbook`
3. Restart Processing IDE
4. Use the library in your sketches

## Configuration

### release.properties

Configure library metadata:

```properties
name=Your Library Name
version=1
prettyVersion=1.0.0
authors=Your Name
url=https://github.com/yourusername/your-library
categories=Animation,Utilities
sentence=Brief description of your library
paragraph=Detailed description of what your library does
```

### Customizing Package Names

1. Rename `src/main/java/com/myDomain/myLibrary/` to your package structure
2. Update package declarations in Java files
3. Update `group` in `build.gradle.kts`
4. Update import statements in examples

## Release Process

### Automated Release (GitHub Actions)

1. Tag a version: `git tag v1.0.0`
2. Push the tag: `git push origin v1.0.0`
3. GitHub Actions automatically builds and creates a release

### Manual Release

1. Run `./gradlew buildReleaseArtifacts`
2. Find artifacts in `release/` directory
3. Upload to GitHub releases

## Complete Example

See `examples/HelloCircles/HelloCircles.pde`:

```processing
import com.myDomain.myLibrary.*;

Grid grid;
Palette palette;

void setup() {
  size(500, 500);
  palette = new Palette(this);
  grid = new Grid(this, palette.getPalette());
}

void draw() {
  background(0);
  grid.show();
  fill(255);
  textSize(30);
  text("Hello Library", 140, 460);
}

void mouseClicked() {
  grid = new Grid(this, palette.getPalette());
}
```

## Dependencies

| Dependency | Version | Scope |
|------------|---------|-------|
| Processing Core | 4.3.1 | Compile Only |
| JUnit 5 | Latest | Test |

## References

- [Library Basics](https://github.com/processing/processing4/wiki/Library-Basics)
- [Library Guidelines](https://github.com/processing/processing4/wiki/Library-Guidelines)
- [Library Overview](https://github.com/processing/processing4/wiki/Library-Overview)
- [Documentation Website](https://processing.github.io/processing-library-template/)

## License

GNU General Public License v2.0
