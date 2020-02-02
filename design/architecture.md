# Architecture

This document provides the rationales behind the architecture used.

## Goals

- Enumerate the main patterns of the architecture.

## Non Goals

- detailed source list
- detailed API description

## Background

This project is done as learning exercise, for evaluating a set of patterns useful
for simulation of physical objects by software.

## High-Level Design

Central to the design is the mapping of physical objects to logical objects. Each
physical object is mapped to a logical twin. Composed physical objects are
mapped to logical objects composed from the contained objects.

The simulation provides a Web User Interface and a Web API.

## Detailed Design

### Simulated Lamp

The lamp simulated has 2 components:
- Power Switch
- Light Bulb

The simulated actions are:
- Set Power Switch to On/Off
- Set Power Switch to Healthy/Fatal
- Set Light Bulb to Healthy/Fatal
- Light Bulb goes Fatal after some time (configurable)

Depending on the history of actions the Light Bulb will be dark or bright
and the Lamp the same.

### State

There are 3 physical objects in this simulation:
- Lamp
- Power Switch
- Light Bulb

Each object has a state. The state changes when a simulation event happens.

The architecture of the Lamp Simulation is based on a state machine composed
of state machines. Each physical object is mapped to a logical object representig it.
Each logical object is implemented as a state machine. The simulaleted actions are
mapped to events changing the state of the object.

Events are method calls on the state machines.

### Object communication

Each object implements 1 receiver channel to receive events.

If an object is depending on another object it can observe the state of the other
by registering as listener to the other providing the receiver channel
(GoF Observer Pattern).

References to other objects are set by the container object (Dependency Injection).

### Web User Interface

The simulation implements a web server, for human control. Each physical object is
mapped to a HTTP DOM object.

### Application Interface

The simulation will provide a web API of URL's accepting request. Request data will
be Json objects.

### Language

Implementation language will be go.

## Alternatives Considered

JavaScript as language has been considered, but was rejected, as go is simpler in use.

## Security Considerations

None.
