# Kotlinx-UUID-Serializer
[UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) serialization implementation using the [Kotlinx](https://github.com/Kotlin/kotlinx.serialization) serialization library.

### Introduction:
Universally Unique Identifiers (UUIDs) are widely used in software development for uniquely identifying information. 
However when it comes to serializing these UUIDs for storage or transmission, a custom solution is often required,
as many serialization libraries, including Kotlinx, do not provide
out-of-the-box support for UUIDs.
This repository provides a custom serializer for UUIDs, enabling their use with the Kotlinx serialization library.

#### Source:

```kotlin
/**
 * Serializer for UUID objects.
 */
object UUIDSerializer : KSerializer<UUID> {
    override val descriptor: SerialDescriptor = PrimitiveSerialDescriptor("UUID", PrimitiveKind.STRING)

    override fun serialize(encoder: Encoder, value: UUID) = encoder.encodeString(value.toString())

    override fun deserialize(decoder: Decoder): UUID = UUID.fromString(decoder.decodeString())
}

/**
 * Represents a serializable UUID, distinguished from non-serializable UUIDs.
 *
 * @property SUUID The type representing the serializable UUID.
 * @see UUID
 * @see UUIDSerializer
 */
typealias SUUID = @Serializable(with = UUIDSerializer::class) UUID

```

#### Example Usage:

```kotlin
data class Person(
    val id: SUUID,
    val firstName: String,
    val lastName: String
)
```
