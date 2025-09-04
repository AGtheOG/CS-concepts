<xaiArtifact artifact_id="85b09f5a-ebc6-4f8b-87ff-749edb01a337" artifact_version_id="add7526e-6098-4493-8880-55079a501996" title="Shallow_vs_Deep_Copy.md" contentType="text/markdown">

# Shallow Copy vs Deep Copy: Explained

## Definition
A **shallow copy** creates a new object, but the references inside it still point to the same nested objects as the original. A **deep copy**, on the other hand, creates a completely independent copy, recursively duplicating all nested objects.

## Analogy
Imagine a classroom attendance sheet. A shallow copy is like duplicating the sheet, but the student names are still linked to the same students. If a student changes their roll number, both sheets reflect the change. A deep copy is like creating an entirely new sheet with separate records—changes to one don’t affect the other.

## Code Illustration

### C++ Example (Copy Constructor)
```cpp
Student s1("Arin", {90, 85});
Student s2 = s1; // Shallow copy (default copy constructor)
s2.marks[0] = 50; // Changes s1's marks too!

// Deep copy: implement custom copy constructor
Student(const Student& other) {
    name = other.name;
    marks = vector<int>(other.marks.begin(), other.marks.end());
}
```

### Python Example
```python
import copy
a = [[1, 2], [3, 4]]
shallow = copy.copy(a)    # Shallow copy
deep = copy.deepcopy(a)   # Deep copy
```

## Real-Life Use Case
- **Shallow Copy**: Useful when multiple references to shared data are needed, like in caching or logging systems, where you want to save memory and avoid duplicating large datasets.
- **Deep Copy**: Essential for scenarios like simulating different outcomes, such as copying a chess board or machine learning model weights, where each simulation must be independent to avoid unintended interference.

## Tradeoff
Shallow copies are faster and more memory-efficient but can cause unintended side effects due to shared references. Deep copies are safer, ensuring complete independence, but they are more computationally expensive. The choice depends on whether data independence is critical for the task.

</xaiArtifact>
