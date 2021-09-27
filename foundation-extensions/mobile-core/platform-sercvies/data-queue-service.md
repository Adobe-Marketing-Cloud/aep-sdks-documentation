# DataQueue Service

## Overview

The `DataQueue Service` provides access to thread-safe FIFO queues. This service is particularly useful when used in conjunction with a `PersistentHitQueue`.

## Usage

The following code snippet shows how to create a `DataQueue` and add a `DataEntity` to the queue.

{% tabs %}
{% tab title="Android" %}

```java
DataQueue dataQueue = ServiceProvider.getInstance().getDataQueueService().getDataQueue(name);
DataEntity dataEntity = new DataEntity(mydata);
dataQueue.add(dataEntity);
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
// Create a `DataQueue`
guard let dataQueue = ServiceProvider.shared.dataQueueService.getDataQueue(label: name) else {
  Log.error(label: "\(name):\(#function)", "Failed to create Data Queue")
  return
}

// Create a `DataEntity`
let entity = DataEntity(data: myData)

// Add entity to `dataQueue`
dataQueue.add(entity)
```

{% endtab %}
{% endtabs %}

## Public Interfaces

{% tabs %}
{% tab title="Android" %}

- DataQueue

​        A Thread-Safe Queue used to store `DataEntity` Objects.

```java
public interface DataQueue {

	/**
	 * Add a new {@link DataEntity} Object to {@link DataQueue}
	 *
	 * @param dataEntity, instance of {@link DataEntity}
	 * @return true if successfully added else false.
	 */
	boolean add(final DataEntity dataEntity);

	/**
	 * Retrieves the head of {@link DataQueue} else returns null if {@link DataQueue} is empty.
	 */
	DataEntity peek();

	/**
	 * Retrieves the first n entries in this {@link DataQueue}. Returns null if {@link DataQueue} is empty.
	 */
	List<DataEntity> peek(final int n);

	/**
	 * Removes the head of this {@link DataQueue}
	 * @return true if successfully removed else returns false.
	 */
	boolean remove();

	/**
	 * Removed the first n elements in this {@link DataQueue}
	 * @return true if successfully removed else returns false.
	 */
	boolean remove(final int n);

	/**
	 * Removes all stored {@link DataEntity} objects.
	 * @return true if successfully removed else returns false.
	 */
	boolean clear();

	/**
	 * Returns the count of {@link DataEntity} objects in this {@link DataQueue}.
	 */
	int count();

	/**
	 * Closes the current {@link DataQueue}.
	 */
	void close();

}
```
- DataEntity

​        Data Model class for entities stored in `DataQueue`.

```java
public final class DataEntity {

	private final String uniqueIdentifier;
	private final Date timestamp;
	private final String data;

	/**
	 * Generates a new {@link DataEntity}
	 *
	 * @param data a {@link String} to be stored in database entity.
	 */
	public DataEntity(final String data) {
    // ...
	}

	/**
	 * Generates a new {@link DataEntity}
	 *
	 * @param data             a {@link String} to be stored in database entity.
	 * @param uniqueIdentifier unique {@link String} value.
	 * @param timestamp        instance of {@link Date} for retrieving {@link Date#getTime()}.
	 */
	public DataEntity(final String uniqueIdentifier, final Date timestamp, final String data) {
		// ...
	}

	public String getUniqueIdentifier() {
		return uniqueIdentifier;
	}

	public Date getTimestamp() {
		return timestamp;
	}

	public String getData() {
		return data;
	}
}
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

- DataQueuing

​        Defines a platform service to be used to initialize `DataQueue` objects.

```swift
public protocol DataQueuing {
    /// Initialize a `DataQueue` object
    /// - Parameter label: the label you assigned to the `DataQueue` at creation time.
    /// - Returns: the object of `DataQueue`, return false if failed to create an object
    func getDataQueue(label: String) -> DataQueue?
}
```
- DataQueue

​        A thread-safe FIFO (First-In-First-Out) queue used to store `DataEntity` objects.

```swift
public protocol DataQueue {
    /// Adds a new `DataEntity` object to `DataQueue`
    /// - Parameter dataEntity: a `DataEntity` object
    @discardableResult
    func add(dataEntity: DataEntity) -> Bool

    /// Retrieves the head of this `DataQueue`, else return nil if the `DataQueue` is empty
    func peek() -> DataEntity?

    /// Retrieves the first `n` entries in this `DataQueue`, else return nil if the `DataQueue` is empty
    func peek(n: Int) -> [DataEntity]?

    /// Removes the head of this `DataQueue`
    @discardableResult
    func remove() -> Bool

    /// Removes the first `n` entities in this `DataQueue`
    @discardableResult
    func remove(n: Int) -> Bool

    /// Removes all stored `DataEntity` object
    @discardableResult
    func clear() -> Bool

    /// Returns the number of `DataEntity` objects in the DataQueue
    func count() -> Int

    /// Closes the current `DataQueue`
    func close()
}
```
- DataEntity

​        Represents an entity type which can be stored in `DataQueue`.

```swift
public class DataEntity: NSObject {
    public let uniqueIdentifier: String
    public let timestamp: Date
    public let data: Data?

    /// Generates a new `DataEntity`
    ///
    /// This init method automatically assigns a random `UUID` to `uniqueIdentifier` and sets `timestamp` to `Date()`
    ///
    /// - Parameters:
    ///   - data: a JSON-encoded representation for `DataEntity`
    public init(data: Data?) {
        // ...
    }

    /// Generates a new `DataEntity`
    /// - Parameters:
    ///   - uniqueIdentifier: a string identifier for `DataEntity`
    ///   - timestamp: a timestamp for `DataEntity`
    ///   - data: a JSON-encoded representation for `DataEntity`
    public init(uniqueIdentifier: String, timestamp: Date, data: Data?) {
        // ...
    }
}
```

{% endtab %}
{% endtabs %}