# 📘 Naming Variables Like a Pro

Naming things in programming is hard. But **good names** make your code  
✅ easier to read  
✅ easier to maintain  
✅ easier to debug  

A simple rule of thumb:  

👉 **Variables = Nouns, Functions = Verbs, Booleans = Adjectives**

---

## 📌 1. Nouns – For Data / Objects
Use **nouns** when the variable holds an entity, object, or structure.  
They represent "things" in your code.  

**Examples:**
```cpp
User user;
Order order;
vector<User> usersList;
map<int, Order> ordersMap;
string errorMessage;
```

✅ Easy to understand: user is a thing, not an action.

## 📌 2. Adjectives – For States / Flags
Use adjectives or descriptive phrases for booleans or condition states.  
They answer “what is true about this?”

**Examples:**
```cpp
bool isActive;
bool isAdmin;
bool hasChildren;
bool canExecute;
bool isValid;
```

✅ Reads naturally: if (isActive) ... feels like English.

## 📌 3. Verbs – For Functions / Methods
Use verbs or verb phrases when naming actions.  
Functions do something.

**Examples:**
```cpp
double calculateTax(double income);
vector<User> fetchUsers();
void sendEmail(string recipient);
void sortList(vector<int>& arr);
```

✅ Clear: you know exactly what each function does.

## 📌 4. Verb + Noun Combos – For Actions on Data
When an action operates on a specific entity, use verb + noun.

**Examples:**
```cpp
string getUserName(User user);
void updateProfile(User& user);
void processQueue(queue<Task>& tasks);
```

✅ Tells both what it does and what it works on.

## 📌 5. Helpful Prefixes & Suffixes
Sometimes, context words make names clearer:

- minValue, maxCount, userId, totalSum
- currNode, prevNode, tempFile
- errorMsg, configPath

✅ Keeps meaning sharp without over-explaining.

## 🎯 Quick Cheat Sheet
| Type | Naming Style | Examples |
|------|--------------|----------|
| Variable (thing) | Noun | user, account, transaction |
| Boolean (state) | Adjective | isActive, hasChildren, canExecute |
| Function (action) | Verb / Verb-Noun | fetchUsers(), calculateTax(), updateProfile() |
| Collections | Plural Noun | usersList, ordersMap, tasksQueue |
| Temporary / Loops | Short / Contextual | i, j, temp, currNode |

## ❌ Bad vs ✅ Good Naming
Bad naming makes code confusing and forces readers to guess.  
Good naming makes code readable like plain English.

**Examples:**

```cpp
// ❌ Bad
int x1; 
bool flag;
void doStuff();

// ✅ Good
int userCount;
bool isLoggedIn;
void fetchUserData();

// ❌ Bad
vector<int> a;
string s1, s2;
bool check;

// ✅ Good
vector<int> orderIds;
string firstName, lastName;
bool isValidUser;
```

## ✨ Golden Rule
If you can read your code like English, you’re naming variables right:

```cpp
if (user.isActive) {
    sendEmail(user);
}
```

✅ Feels natural. No extra comment needed.

## 💡 Final Checklist
Next time you write code, ask yourself:
- Is this a thing → noun
- Is this a state → adjective
- Is this an action → verb

That’s it! Simple, clean, and professional.

</xaiArtifact>
