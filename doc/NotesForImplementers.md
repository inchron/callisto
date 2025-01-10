# Notes for Implementers

You are free to use the callisto.ecore in your own applications. To ensure 
interopability, there are some rules to be considered regarding the serialization of 
models as XMI.

## Platform Dependent Types

We are aware that common types like time or frequency are already used in many tools.
These types are therefor defined in a subpackage _platform_. To use your own types, 
you can ignore this subpackage, and change references like 
RuleSetParam.overhead to point to your own definition of an EClass Time.

The only requirement is that the serialization conforms to the format defined in the 
callisto.ecore.

## Working with Standard EMF Tools
All models (i.e. instances of the meta model specified in callisto.ecore) can be created and edited with standard EMF tooling. The general steps required to generate an Editor are described here:
https://www.vogella.com/tutorials/EclipseEMF/article.html

The generation of the Editor itself is described in section "5. Create EMF Editor plug-ins".

As this repository contains the .ecore files only, the required genmodel has to be created as described in section "11. Create EMF Generator Model".

## Default Serialization for Basic Types

Many classes in the callisto.ecore are derived from the platform/ModelObject class. 
It's only purpose is to provide a _name_ attribute (EString) and an attribute 
_intrinsicId_ (EString). The serialization, e.g. of a CoreType in a (hypothical) 
container Project.coretypes, should look like:

```xml
<coretypes name="SampleName" intrinsicId="_123[...]xyz" ... />
```

The attribute _intrinsicId_ is also configured with EAttribute.iD = true. Any ecore 
based modelling framework will use its value in inter- and intra-document references. 
We recommend to use a Globally Unique Identifier (GUID) for this purpose. In a C++/Qt 
application this could be done as:

```c++
ModelObject::ModelObject() {
    QString uuid(
            QUuid::createUuid().toRfc4122().toBase64(
                    QByteArray::Base64Encoding
                            | QByteArray::OmitTrailingEquals));
    m_intrinsicId = uuid.prepend("_").toStdString();
}
```

References for unique identifiers in an ecore and XMI context:
[EcoreUtil.generateUUID()](https://download.eclipse.org/modeling/emf/emf/javadoc/2.5.0/org/eclipse/emf/ecore/util/EcoreUtil.html#generateUUID())
[XML NCName](https://www.w3.org/TR/1999/REC-xml-names-19990114/#NT-NCName)


Time values shall be serialized as follows, e.g. for RuleSetParam.overhead:

```xml
<overhead value="<INTEGER>" unit="<TIMEUNIT>" />
```
For applications, which use scalar variables to represent time, we recommend to define
a wrapper class with a fixed unit (e.g. picoseconds or ticks). All time values in a
callisto model are containment EReferences, not EAttributes.

Similarly, Frequency values are modeled as objects, too, and serialized as follows, e.g. 
for a CoreType.frequency:

```xml
<frequency  value="<INTEGER>" unit="<FREQUENCYUNIT>" />
```
