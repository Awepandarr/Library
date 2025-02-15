# Library
```mermaid
classDiagram
    class Zoo {
        - name: String
        - location: String
        - animals: List<Animal>
        - enclosures: List<Enclosure>
        - staff: List<Staff>
        + addAnimal(animal: Animal): void
        + removeAnimal(animal: Animal): void
        + assignEnclosure(animal: Animal, enclosure: Enclosure): void
        + assignStaff(staff: Staff): void
    }

    class Animal {
        - id: String
        - name: String
        - species: Species
        - type: String
        - healthStatus: String
        - enclosure: Enclosure
        + getDetails(): String
        + updateHealthStatus(status: String): void
        + assignEnclosure(enclosure: Enclosure): void
    }

    class Species {
        - name: String
        - scientificName: String
        - diet: String
        - lifespan: String
        + getSpeciesInfo(): String
    }

    class Enclosure {
        - id: String
        - habitat: String
        - size: Double
        - environmentalConditions: String
        - animalCapacity: Integer
        + addAnimal(animal: Animal): void
        + removeAnimal(animal: Animal): void
        + checkCapacity(): Boolean
    }

    class Staff {
        - employeeID: String
        - name: String
        - role: String
        - contactInfo: String
        + assignRole(role: String): void
    }

    class Veterinarian {
        - employeeID: String
        - name: String
        - expertise: String
        + diagnoseAnimal(animal: Animal): String
        + treatAnimal(animal: Animal): void
    }

    Zoo "1" -- "many" Animal : contains
    Zoo "1" -- "many" Enclosure : has
    Zoo "1" -- "many" Staff : employs
    Animal "1" -- "1" Species : belongs to
    Animal "1" -- "1" Enclosure : housed in
    Staff "1" -- "many" Veterinarian : manages
    Enclosure "1" -- "many" Animal : houses
    Veterinarian "1" -- "many" Animal : treats
