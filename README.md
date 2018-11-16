# Sdcb.System.Range
Provide System.Index, System.Range for C# 8.0.

This file is almostly copied from following url:
* https://github.com/dotnet/csharplang/blob/master/proposals/ranges.cs
* https://csharp.christiannagel.com/2018/07/24/indexesandranges/

Index example:
```
var last = ^1;
int[] arr = { 1, 2, 3 };
int lastItem = arr[last];
Console.WriteLine(lastItem); // 3

int lastItem2 = arr[arr.Length - 1];
Console.WriteLine(lastItem2); // 3
```

Range example:
```
// Old school: 
string text1 = "the quick brown fox jumped over the lazy dogs";
string lazyDogs1 = text1.Substring(36, 9);
string lazyDogs2 = text1.Substring(text1.Length - 9, 9);

// Range style: 
string lazyDogs3 = text1[^9..^0];  // lazy dogs

// lazyDogs4 is exactly the same as lazyDogs3
var start = ^9;
var end = ^0;
var range = Range.Create(start, end);
string lazyDogs4 = text1.Substring(range);

// Other usages:
string lazyDogs5 = text1[^9..];  // Range.FromStart
string lazyDogs6 = text1[36..]; // Range.FromStart
string thequick = text1[..9]; // Range.ToEnd
string completeString = text1[..]; // Range.All

// Ranges with array: 
var arr = new[] { 1, 4, 8, 11, 19, 31 };
var range = arr[2..5];
ref int elt = ref range[1];
elt = 42;
int copiedelement = range[1];
copiedelement = 11;
Console.WriteLine($"the original element is changed: {arr[3]}"); // 42
```
