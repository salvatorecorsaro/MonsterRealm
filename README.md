# 🐉 MonsterRealm - A Monster and Hero learning project 🛡️


![main image](monsterrealm.png)

## 🌟 Theme

Welcome to **MonsterRealm**, a spellbinding platform where you can summon monsters and heroes for epic battles! Whether a monster wins or loses is determined by the valorous heroes who step up to the challenge. A fantastic learning playground for those intrigued by Spring Boot, RESTful APIs, and Kafka messaging.

---

## 🏗️ Microservices

### 1️⃣ **Monster Service** 
- **Role**: Handles CRUD operations for monsters. 
- **Technologies**: Spring Boot, JPA, Kafka Producer API
- **Kafka Events Produced**: `MonsterCreatedEvent`
  
#### 🎯 Functionalities

- 🐾 Create a new monster
- 🔍 Retrieve monster details
- 📜 List all monsters

#### 📡 REST API Endpoints

- `POST /api/monsters` - 🆕 Create a new monster
- `GET /api/monsters/{id}` - 🔍 Retrieve a monster by its ID
- `GET /api/monsters` - 📜 List all monsters

---

### 2️⃣ **Hero Service** 
- **Role**: Manages CRUD operations for heroes.
- **Technologies**: Spring Boot, JPA, Kafka Consumer API
- **Kafka Events Consumed**: `MonsterCreatedEvent`
  
#### 🎯 Functionalities

- 🦸 Create a new hero
- ✏️ Update a hero
- 🔍 Retrieve hero details
- ❌ Delete a hero
- 📜 List all heroes

#### 📡 REST API Endpoints

- `POST /api/heroes` - 🦸 Create a new hero
- `PUT /api/heroes/{id}` - ✏️ Update a hero
- `GET /api/heroes/{id}` - 🔍 Retrieve a hero
- `DELETE /api/heroes/{id}` - ❌ Delete a hero
- `GET /api/heroes` - 📜 List all heroes

---

## 💻 Class and Event Examples

### 🐾 Monster Class

```java
public class Monster {
    private Long id;
    private String name;
    private String type;
    private String status; // "Won" or "Lost"

    // Getters and Setters
}
```

### 🦸 Hero Class

```java
public class Hero {
    private Long id;
    private String name;
    private String ability;
    private Integer battlesFought;

    // Getters and Setters
}
```

### 📨 Kafka Events

#### MonsterCreatedEvent

```java
public class MonsterCreatedEvent {
    private Long monsterId;
    private String name;

    // Getters and Setters
}
```

#### BattleOutcomeEvent

```java
public class BattleOutcomeEvent {
    private Long monsterId;
    private String outcome; // "Won" or "Lost"

    // Getters and Setters
}
```

---

## 📫 Communication via Kafka

### 📢 Kafka Topics

- 🆕 `monster_created_topic` - For new monsters
- 🥇 `battle_outcome_topic` - For battle outcomes (Monster Wins/Loses)

### 🔄 Event Interaction

1️⃣ **When a New Monster is Created:**
  - **Monster Service**: 🐾 Creates a monster and sends a `MonsterCreatedEvent`.
  - **Hero Service**: 🦸‍♀️ Listens and selects up to 4 heroes for the battle.
  - 🎲 Battle outcome is based on the number of heroes:
    - 0 heroes ➡️ Monster Wins 🎉
    - 1-4 heroes ➡️ Victory odds increase with more heroes 🛡️

2️⃣ **Battle Outcome:**
  - **Hero Service**: 📣 Announces the outcome via `BattleOutcomeEvent`.
  - **Monster Service**: 📝 Updates monster's status as "Won" or "Lost".

---

## 🎓 Learning Objectives

1️⃣ Master the architecture of microservices.  
2️⃣ Get hands-on experience with RESTful APIs using Spring Boot.  
3️⃣ Perform CRUD operations with JPA/Hibernate.  
4️⃣ Dive into Kafka messaging.  