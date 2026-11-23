# ECOSYSTEM UPGRADES
The following post will go over a plethora of Ecosystem Upgrades that would be extremely valuable for customizing each individual Ecosystem to the needs of their community. This will include an Ideal Implementation of these alongside a description of what each item is for, and how it would take effect on the site, and or Mod Managers, if they choose to respect the Ecosystem.

## Section-Based
This will go over things that would be nice as an upgrade to the sectioning system for the Ecosystem. Right now this is what a Section looks like within the Ecosystem. This one in particular is sourced from a PR to add the new TCG Card Shop Simulator Branch as a section on the site, like we have with other branches for our Ecosystem.

```yml
    1-0-new-render-modpacks:
      name: "1.0 New Render Branch Modpacks"
      requireCategories:
        - "modpacks"
        - "1-0-new-render-branch"
      excludeCategories:
        - "tools"
```

How this works for someone who is not as tech savvy would be as follows:

* First define the Internal Name, this is what the string of text at the start of the section is.
* Second define the Name in which is shown for the Section itself, it must be in `"` because it is a literal string. This is how you get display names that don't match the underlying category ID.
* Third, default filtering, this is the Primary Purpose of the Sections, they basically act as a filtered view of the Ecosystems content. For example here we require items to both bear the categories `modpacks` and `1-0-new-render-branch`, these come from the internal name for each category that would be a part of the ecosystem. Here we are also excluding a specific category, that category being `tools`. In this case the exclusion is used in order to refine tools to a specific section under the Ecosystems Sections Field. **NOTE THESE ARE NOT REQUIRED TO MAKE A SECTION, AND YOU DON'T NEED BOTH FOR IT TO BE VALID EITHER.**

Now what can be different here, or help improve this system? Well the following:

* [Section Category Defaults](#section-category-defaults)
* [Section Specific Categories](#section-specific-categories)
* [Section-Based Hidden Categories](#section-based-hidden-categories)
* [Required and Excluded Concatenation Toggle](#required-and-excluded-concatenation-toggle)
* [Required and Excluded Categories with a Lock Icon and Reflected State](#required-and-excluded-categories-with-a-lock-icon-and-reflected-state)
* Section Core Categories; See the Categories Section.

### Section Category Defaults
What does this entail, well it would entail the following:

* The Ability to have certain Categories set to Exclude or Included by default for the Section.
* The Ability for these Categories to be toggled back to Included or Excluded by the User's discretion.
* The Ability to have Optional-Filters with Defaults for the Section.

My thinking of how this could look within the schema is the following, which would be directly under the given section:

```yml
        category-defaults:
            - category: "ai-generated"
              default-visibility: false
            - category: "tools"
              default-visibility: true
```

Heres how this works:

* First off you define the `category-defaults` array. As shown in Line one, every item will start with a dash, and will contain two values.
* Now, these values what do they mean?
    * `category` is the internal name or identifier of the given Category.
    * `default-visibility` is the bool that will determine whether or not this category should be forced as `Included` (true) or `Excluded` (false) by default
* To finish this off, on the site and in mod managers respecting how sections work, this would by default exclude or include the specified category when viewing this section. It is not locked into this state, however it is togglable by the user if they want to force inclusion or exclusion of the specific Category.

### Section Specific Categories
What does this entail, well it would entail the following:

* The Ability to make Subcategories that are **Specific** to this Category, that would not show up as filters in any other context. Except the Global Database.
* The Ability to have finer filtering for a Section of Content. Note the use of `Content` here, this is mainly for the case where an Ecosystem has other forms of Modifications that are not MODs. As an example Developer Tools, Worlds, Universes, Saves, Asset Packs, Audio Packs etc. These cases are courtesy of the Hytale Ecosystem specifically, but other Ecosystems may have similar structures.
* The Ability to have Categories outside of the Main Category List.

My thinking of how this could look within the schema is the following, which would be directly under the given section:

```yml
        section-categories:
            adventure:
                label: "Adventure"
            creation:
                label: "Creation"
            minigame:
                label: "Minigame"
            modded:
                label: "Modded"
            parkour:
                label: "Parkour"
            puzzle:
                label: "Puzzle"
            survival:
                label: "Survival"
            horror:
                label: "Horror"
            fantasy:
                label: "Fantasy"
            sci-fi:
                label: "Sci-Fi"
```

Here's how this works:

* First off you define the `section-categories` array. As shown in Line one, every item in this case would not start with a `-`, this is to mirror the `categories` field of the Ecosystem.
* Each Category would be defined the same way as your normal category, e.g. with a label AND what will be covered in the Categories section of this Post.
* These Categories would appear in their own filtering section named after the Section itself. E.G. An `Worlds Categories` section, and under it would be each of the categories defined beneath this section.
* When uploading if the Sections Core Category is used (in this case Worlds), it would prompt the user to add Categories that match the specific world, based on the sections pool of Categories.
* These categories would NOT show up elsewhere, unless the Sections Core Category is included.

### Section-Based Hidden Categories

### Required and Excluded Concatenation Toggle

### Required and Excluded Categories with a Lock Icon and Reflected State
