# Routine Algorithms
This file implements some routine algorithms.


## Utility Functions
### FileExist
`FileExist` checks whether a file named `filename` exists, returns true if it exists, returns false if not.
```
inline bool FileExist(const std::string& filename);
```

### FormatToHexString
`FormatToHexString` formats the input `byte_str` which is an octet string to a hexadecimal string. 
```
std::string FormatToHexString(std::string byte_str);
```

### IsPowerOfTwo
`IsPowerOfTwo` checks whether there exists an integer $n$ satisfies $x = 2^n$ for $x > 0$, returns true if integer $n$ exists, returns false if not.
```
bool IsPowerOfTwo(size_t x);
```

### GenRandomIntegerVectorLessThan
`GenRandomIntegerVectorLessThan` returns a random integer vector. The vector generated in this way does not require cryptographic security. 
```
std::vector<int64_t> GenRandomIntegerVectorLessThan(size_t LEN, int64_t MAX);
```
 *  `size_t LEN`: the length of the generated integer vector.
 * `int64_t MAX`: the range of each value in the generated vector is limited to [0,...,MAX].


## Operator Overloading 
We provide serialization in many places, so we need to overload operator `>>` and `<<` to deal with different input/output stream objects, such as `ElementType` including any C++ POD type, and `std::vector<ElementType>`.
```
template <typename ElementType> std::ofstream &operator<<(std::ofstream &fout, const ElementType& element);
template <typename ElementType> std::ifstream &operator>>(std::ifstream &fin, ElementType& element);

template <typename ElementType> 
std::ofstream &operator<<(std::ofstream &fout, const std::vector<ElementType>& vec_element);
template <typename ElementType> 
std::ifstream &operator>>(std::ifstream &fin, std::vector<ElementType>& vec_element);

template < > std::ofstream &operator<<<std::string>(std::ofstream &fout, const std::string& str);
template < > std::ifstream &operator>><std::string>(std::ifstream &fin, std::string& str);
```

Note: if the input/output stream object is string, it will call the specialized template function. 