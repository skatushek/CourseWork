# CourseWork
﻿<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
# C# Coursework: Library Management System

## Person.cs

```csharp
using System;

namespace LibrarySystem
{
    public class Person
    {
        protected string name;

        public Person(string inputName)
        {
            name = inputName;
        }

        public virtual string GetInfo()
        {
            return $"Person: {name}";
        }
    }
}
```

## Member.cs

```csharp
namespace LibrarySystem
{
    public class Member : Person
    {
        protected int memberId;

        public Member(string inputName, int inputId) : base(inputName)
        {
            memberId = inputId;
        }

        public override string GetInfo()
        {
            return $"Member {name} with ID {memberId}";
        }
    }
}
```

## StudentMember.cs

```csharp
namespace LibrarySystem
{
    public class StudentMember : Member
    {
        public StudentMember(string inputName, int inputId)
            : base(inputName, inputId)
        {
        }

        public override string GetInfo()
        {
            return $"Student {name} with ID {memberId}";
        }
    }
}
```

## PremiumMember.cs

```csharp
namespace LibrarySystem
{
    public class PremiumMember : Member
    {
        public PremiumMember(string inputName, int inputId)
            : base(inputName, inputId)
        {
        }

        public override string GetInfo()
        {
            return $"Premium member {name} with ID {memberId}";
        }
    }
}
```

## Utility.cs

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace LibrarySystem
{
    public static class Utility
    {
        public static T FindMaximum<T>(List<T> values) where T : IComparable<T>
        {
            if (values.Count == 0)
            {
                throw new Exception("Container is empty");
            }

            return values.Max();
        }
    }
}
```

## Program.cs

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace LibrarySystem
{
    class Program
    {
        static void Main()
        {
            List<Person> members = new List<Person>
            {
                new StudentMember("Alice", 101),
                new PremiumMember("Bob", 202),
                new Member("Charlie", 303)
            };

            foreach (Person member in members)
            {
                Console.WriteLine(member.GetInfo());
            }

            List<int> borrowedBooks = new List<int> { 5, 8, 3, 10 };

            try
            {
                Console.WriteLine("Maximum borrowed books: " + Utility.FindMaximum(borrowedBooks));
            }
            catch (Exception error)
            {
                Console.WriteLine(error.Message);
            }

            borrowedBooks.Sort();
            borrowedBooks.Reverse();
        }
    }
}
```

