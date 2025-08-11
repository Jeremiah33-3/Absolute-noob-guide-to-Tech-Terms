# Software Design

2 aspects ([CREDITS](https://nus-cs2103-ay2425s2.github.io/website/se-book-adapted/chapters/design.html)):
1. Product/external design: designing the external behavior of the product to meet the users' requirements. (usually done by product designers with input from business analysts, user experience experts, user representatives, etc.)
2. Implementation/internal design: designing how the product will be implemented to meet the required external behavior. (usually done by software architects and software engineers.)

## Software Architecture

> The software architecture of a program or computing system is the structure or structures of the system, which comprise software elements, the externally visible properties of those elements, and the relationships among them. Architecture is concerned with the public side of interfaces; private details of elements—details having to do solely with internal implementation—are not architectural. -- Software Architecture in Practice (2nd edition), Bass, Clements, and Kazman

Very high level design. Usually consists of a set of interacting components that fit together for a functionality. Can be encapsulated in [architectural diagrams](https://www.lucidchart.com/blog/how-to-draw-architectural-diagrams). 

## Modelling

Models is the representation of something, usually provides a simpler view of complex entity. In software devlopment, models are useful to analyse complex entities related to the software system, communicate information among stakeholders, and be used as a blueprint for creating softwares.

Software architectures can be encapsulated in diagrams, other diagrammable aspects of the softwares include structures and behaviours of the system, as formalised by Unified Modelling Language ([UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language)).

### 🏛️ **Architectural Diagrams**
These are **high-level representations** of a system's structure. They focus on how components interact, where they are deployed, and how data flows across the system.

#### **Purpose:**
- To communicate the **overall structure** of a system.
- To show **components**, **services**, **databases**, **external systems**, and **deployment environments**.
- Often used by **software architects**, **DevOps**, and **stakeholders**.

#### **Types:**
- **System architecture diagram**/**application architecture diagram**
- **Deployment diagram** (can overlap with UML)
- **Integration architecutral diagram** (components interactions)
- **Infrastructure diagram** (e.g., cloud architecture)
- **Data flow diagram**/**Data architecture diagram** (how and where data flows, processed, used, collected, stored --> data structures visualisations, optimisation strategies strategies)
- **DevOps architecture diagram** (process flow diagrams, operational flows)
- **Microservices architecture**

#### How to
A guide [here](https://www.geeksforgeeks.org/system-design/how-to-draw-architecture-diagrams/).

#### **Tools:**
- Draw.io, [Lucidchart](https://www.lucidchart.com/blog/how-to-draw-architectural-diagrams), Microsoft Visio, AWS Architecture Icons, etc.

---

### 🧩 **UML Diagrams**
UML is a **standardized modeling language** used to specify, visualize, and document software system design.

#### **Purpose:**
- To model **software behavior**, **structure**, and **interactions**.
- More detailed and formal than architectural diagrams.
- Used by **developers**, **system analysts**, and **designers**.

#### **Types:**
UML includes **14 diagram types**, grouped into:
- **Structural diagrams**: Class, Object, Component, Deployment, Composite Structure, Package, Profile
- **Behavioral diagrams**: Use Case, Sequence, Activity, State Machine, Interaction, Communication, Interaction Overview, Timing

#### **Tools:**
- StarUML, Enterprise Architect, Visual Paradigm, PlantUML, etc.

---

### 🔍 **Key Differences**
| Aspect | Architectural Diagrams | UML Diagrams |
|--------|------------------------|--------------|
| **Focus** | System-level structure | Software-level design |
| **Audience** | Architects, stakeholders | Developers, analysts |
| **Formality** | Informal or semi-formal | Formal, standardized |
| **Scope** | Broad (includes hardware, cloud, etc.) | Narrower (software design) |
| **Customization** | Highly customizable | Follows UML standards |

---
