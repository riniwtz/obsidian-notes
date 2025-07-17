---

---

---
## Get Collection Reference from Collection Name
```typescript
// Get Collection Reference
const usersCollectionRef: CollectionReference<DocumentData> = collection(db, collectionName);
```


## Get Document Reference from Collection Name and Document ID

```typescript
// Get Document Reference from Collection Name and Document ID
const specificUserDocRef: DocumentReference<DocumentData> = doc(db, collectionName, documentId);
```

## Get Subcollection from Document
```typescript
// Get Subcollection Reference
const usersCollectionRef: CollectionReference<DocumentData> = collection(documentRef, collectionName);
```

## Get Doc from Subcollection (Direct)
```typescript
doc(db, 'events-backup', eventId, 'guests', row.original.uid);
// is equivalent to /events-backup/{eventId}/guests/{uid}
// instead of collection(doc(db, 'guests-backup', docId), 'guest')
```

## Query
```typescript
// query(query: Query<unknown, DocumentData>, compositeFilter: QueryCompositeFilterConstraint, ...queryConstraints: QueryNonFilterConstraint[]): Query<unknown, DocumentData>

query(collectionRef, ...queryConstraints)

// queryConstraints include where, orderBy, limit, etc. functions
```


---
```typescript

await getDoc(doc(db, 'events-backup', id));
await getDocs(query(collection(db, 'events-backup'), where('id', '==', id)));
```


```
<!-- Ticket Deadline -->

{#if event.deadline}

<div class="flex items-center gap-3">

<div class="bg-primary flex aspect-square h-9 items-center justify-center rounded-sm">

<Fa icon={faTicket} class="text-white" />

</div>

<div class="flex flex-col">

<!-- Deadline Title -->

<!-- <p class="text-md font-bold">

{event.dead}

</p> -->

<!-- Socials -->

<!-- <a class="text-xs text-blue-500 underline" href={event.eventInstagram}>

{event.deadline}

</a> -->

</div>

</div>

{/if}
```