{
  "cells": [
    {
      "cell_type": "markdown",
      "source": [
        "# Dynamic Access and Modification of Object Attributes in Python\n",
        "\n",
        "Code:\n",
        "\n",
        "<a href=\"https://colab.research.google.com/drive/1oSTMYFMHq0Y60SR-IzLYiS78nFpEvrlP\"\n",
        "  target=\"_parent\">\n",
        "  <img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"To run open In Colab\"/>\n",
        "</a>\n",
        "\n",
        "---\n",
        "\n",
        "Written By:\n",
        "[Prabin Raj Shrestha](mailto:prabin.r.shrestha@gmail.com)\n",
        "\n",
        "pshres01@syr.edu | [linkedin.com/in/prbnrs](linkedin.com/in/prbnrs) | [github.com/Prbn](github.com/Prbn)\n",
        "\n",
        "<a href=\"https://www.linkedin.com/in/prbnrs/\" target=\"_blank\">\n",
        "  <img src=\"https://content.linkedin.com/content/dam/me/business/en-us/amp/brand-site/v2/bg/LI-Bug.svg.original.svg\"\n",
        "  alt=\"LinkedIn of Prabin Raj Shrestha\"\n",
        "  width=\"100\" height=\"100\"/>\n",
        "</a>\n",
        "<a href=\"https://github.com/Prbn/Profile/blob/main/README.md\" target=\"_blank\">\n",
        "  <img src=\"https://raw.githubusercontent.com/gilbarbara/logos/29e8719bf78915c7a82a26a6c203f53c4cb8fff2/logos/github.svg\"\n",
        "  alt=\"GitHub of Prabin Raj Shrestha\"\n",
        "  width=\"200\" height=\"100\"/>\n",
        "</a>\n",
        "\n",
        "---\n",
        "\n"
      ],
      "metadata": {
        "id": "QpOrKqKT9YLd"
      },
      "id": "QpOrKqKT9YLd"
    },
    {
      "cell_type": "markdown",
      "id": "1e398fc6",
      "metadata": {
        "id": "1e398fc6"
      },
      "source": [
        "## Introduction\n",
        "In this notebook, we'll learn how to dynamically access and change object attributes during runtime in Python\n",
        "\n",
        "There are four functions in Python that allow us to dynamically access and change attributes of objects during runtime:\n",
        "1. `getattr()`\n",
        "2. `setattr()`\n",
        "3. `hasattr()`\n",
        "4. `delattr()`"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 1,
      "id": "13aa574c",
      "metadata": {
        "id": "13aa574c"
      },
      "outputs": [],
      "source": [
        "# Simple class example\n",
        "class Person:\n",
        "    def __init__(self, name, age):\n",
        "        self.name = name\n",
        "        self.age = age"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "ea2c565a",
      "metadata": {
        "id": "ea2c565a"
      },
      "source": [
        "### Creating and Printing an Object\n",
        "Let's create a `Person` object and print its attributes."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 2,
      "id": "8b766d0b",
      "metadata": {
        "id": "8b766d0b",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "556f6479-5fe2-4dc0-ec98-bd1b0cfb422b"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Raj\n",
            "25\n"
          ]
        }
      ],
      "source": [
        "p = Person(\"Raj\", 25)\n",
        "print(p.name)  # Output: Raj\n",
        "print(p.age)   # Output: 25"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "dd6df079",
      "metadata": {
        "id": "dd6df079"
      },
      "source": [
        "### Dynamic Access in Data Structures\n",
        "In pandas, we can access DataFrame columns dynamically using dictionary-like syntax. This idea can be extended to class attributes."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 3,
      "id": "46f6f128",
      "metadata": {
        "id": "46f6f128",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "80b24bfc-f6e7-4295-9f3a-48fa0997d826"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "0    1\n",
            "1    2\n",
            "2    3\n",
            "Name: column_name, dtype: int64\n"
          ]
        }
      ],
      "source": [
        "import pandas as pd\n",
        "\n",
        "# Example DataFrame\n",
        "df = pd.DataFrame({'column_name': [1, 2, 3]})\n",
        "print(df['column_name'])  # Dynamic column access in pandas"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "832033ac",
      "metadata": {
        "id": "832033ac"
      },
      "source": [
        "## Dynamic Attribute Access\n",
        "Unlike dictionaries, you can't dynamically access class attributes using subscript notation. For dynamic access, we can use the `getattr` function.\n",
        "\n",
        "we can use `getattr()` to dynamically access attributes during runtime based on user input or certain conditions.\n",
        "\n",
        "The `setattr()` function allows us to dynamically set the attributes of an object. This is useful when the attribute name and value are determined at runtime.\n",
        "\n",
        "\n",
        "Syntax: `getattr(object, attribute_name, default_value)`\n",
        "\n",
        "- `object`: The object from which you want to get the attribute.\n",
        "- `attribute_name`: The name of the attribute you want to access.\n",
        "- `default_value`: The value to return if the attribute does not exist (optional).\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 4,
      "id": "54095a37",
      "metadata": {
        "id": "54095a37",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "5f1a81e2-749c-4c55-9856-f22b97b4ce18"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Raj\n"
          ]
        }
      ],
      "source": [
        "# @title Example: Access Attribute\n",
        "\n",
        "# choice = input(\"Which attribute do you want to access? \")\n",
        "choice = \"name\" # For example, user wants to access 'name'\n",
        "\n",
        "print(getattr(p, choice, 'Non-existent'))"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "074eea4f",
      "metadata": {
        "id": "074eea4f"
      },
      "source": [
        "## Dynamic Attribute Setting\n",
        "We can also dynamically set attributes using the `setattr` function.\n",
        "\n",
        "Syntax: `setattr(object, attribute_name, value)`\n",
        "\n",
        "- `object`: The object on which you want to set the attribute.\n",
        "- `attribute_name`: The name of the attribute you want to set.\n",
        "- `value`: The value to set for the attribute."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 5,
      "id": "27983415",
      "metadata": {
        "id": "27983415",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "fdc5935f-abd2-4a27-b083-3d3ede87b14a"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "name has been set to Aman\n"
          ]
        }
      ],
      "source": [
        "# @title Example: Set Attribute\n",
        "\n",
        "# choice = input(\"Which attribute do you want to change? \")\n",
        "# value = input(\"What do you want to change this to? \")\n",
        "\n",
        "choice = \"name\"  # For example, user wants to change 'name'\n",
        "new_value = \"Aman\"  # New value for the attribute\n",
        "\n",
        "setattr(p, choice, new_value)\n",
        "\n",
        "print(f\"{choice} has been set to {new_value}\")"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "0b5308c3",
      "metadata": {
        "id": "0b5308c3"
      },
      "source": [
        "### Creating New Attributes\n",
        "You can even create new attributes dynamically."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 6,
      "id": "4ed4b2d7",
      "metadata": {
        "id": "4ed4b2d7",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "36cb47f2-b0e6-4c79-fbcc-b6119e4d6f46"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "180\n"
          ]
        }
      ],
      "source": [
        "# @title Example: Set New Attribute\n",
        "\n",
        "# new_att_name = input(\"New Attribute Name: \")\n",
        "# new_att_value = input(\"New Attribute Value: \")\n",
        "\n",
        "new_att_name = 'height'\n",
        "new_att_value = 180\n",
        "\n",
        "setattr(p, new_att_name, new_att_value)\n",
        "\n",
        "\n",
        "print(getattr(p, new_att_name, new_att_value)) # Output: 180"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "09853d7d",
      "metadata": {
        "id": "09853d7d"
      },
      "source": [
        "## Checking Attributes\n",
        "\n",
        "For checking attributes we can use the function `hasattr`\n",
        "\n",
        "The `hasattr()` function allows us to check if an attribute exists in an object. This is useful for validating the existence of an attribute before performing operations on it.\n",
        "\n",
        "Syntax: `hasattr(object, attribute_name)`\n",
        "\n",
        "- `object`: The object on which you want to check the attribute.\n",
        "- `attribute_name`: The name of the attribute to check."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 7,
      "id": "602c74a1",
      "metadata": {
        "id": "602c74a1",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "23100521-d9db-4b86-e933-9eda525c0f5a"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Attribute 'age' exists: True\n"
          ]
        }
      ],
      "source": [
        "# @title Example: Checking Attribute\n",
        "\n",
        "# choice = input(\"Which attribute do you want to check? \")\n",
        "\n",
        "choice = \"age\"  # For example, user wants to check if 'age' exists\n",
        "exists = hasattr(p, choice)\n",
        "print(f\"Attribute '{choice}' exists: {exists}\")"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "4d63a463",
      "metadata": {
        "id": "4d63a463"
      },
      "source": [
        "## Deleting Attributes\n",
        "\n",
        "For deleting attributes we can use the function `delattr`\n",
        "\n",
        "The `delattr()` function allows us to delete an attribute from an object. This is useful when you need to remove attributes dynamically.\n",
        "\n",
        "Syntax: `delattr(object, attribute_name)`\n",
        "\n",
        "- `object`: The object from which you want to delete the attribute.\n",
        "- `attribute_name`: The name of the attribute to delete."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 8,
      "id": "309e1f45",
      "metadata": {
        "id": "309e1f45",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "b7e4a712-1656-40ba-825a-5201b2f814b4"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Deleted attribute 'age'\n"
          ]
        }
      ],
      "source": [
        "# @title Example: Deleting Attribute\n",
        "\n",
        "# choice = input(\"Which attribute do you want to check? \")\n",
        "\n",
        "choice = \"age\"  # For example, user wants to delete 'age'\n",
        "if hasattr(p, choice):\n",
        "    delattr(p, choice)\n",
        "    print(f\"Deleted attribute '{choice}'\")\n",
        "else:\n",
        "    print(f\"Attribute '{choice}' does not exist\")"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "7e59a6cd",
      "metadata": {
        "id": "7e59a6cd"
      },
      "source": [
        "We demonstrated how to dynamically access and modify object attributes in Python using `getattr()`, `setattr()`, `hasattr()`, and `delattr()`. These functions provide flexibility for handling object attributes based on runtime conditions, user input, or other dynamic sources.\n",
        "\n",
        "That's how you can dynamically get, set, check, and delete attributes in Python during runtime."
      ]
    },
    {
      "cell_type": "markdown",
      "id": "8136e5c5",
      "metadata": {
        "id": "8136e5c5"
      },
      "source": [
        "---"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "daa04bbb",
      "metadata": {
        "id": "daa04bbb"
      },
      "source": [
        "---\n",
        "---"
      ]
    }
  ],
  "metadata": {
    "language_info": {
      "name": "python"
    },
    "colab": {
      "provenance": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 5
}
