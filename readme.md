
DEPENDENCIES
------------------
pip install south

pip install django-cron

pip install django-csvimport

pip install django-localflavor


About the General App
---------------------
This app is divided in 5 general types of information (Beings, Arts, Spaces, Artworks and Concepts), using a basic Class for each and then several Subclasses to meet the organisational purposes. Sometimes the basic Class is 'abstract' (without an own db table), and so their first Subclasses are creating real db tables and unique ID's for each row. That is for dividing up the unique id creation to each subclass, instead of unique id's for the whole basic types (if they are going to be too much Big tables, and we don't need uid's to avoid conflicts).

To start using the General app in a new database, the recommended starting process will be:

- 1- Create a Concept called 'Type' (using the 'Concepts' admin view).

- 2- Create 3 basic types (using the 'Types' admin view) as:

  - 2.1- 'Being' (or Entity)

  - 2.2- 'Artwork' (or Creation)

  - 2.3- 'Space' (or Place)

  - These 3 types must be assigned to be under 'Type' concept, using the 'parent' field (generating a hierarchical tree). Also we can define the name of the django class-model for each type (nowadays only for remember purposes): 'Being' class for the Being type, 'Artwork' class for the Artwork type and 'Space' class for the Space type.

- 3- Inside 'Being_Types', create a subtype called 'Human', assign the parent type to be 'Being' and the related class to be 'Human'.

- 4- Inside 'Being_Types', create 3 more subtypes under Human parent:

  - 4.1- 'Person' (related class: 'Person').

  - 4.2- 'Project' (related class: 'Project').

  - 4.3- 'Company' (related class: 'Company').

- 5- Inside 'Artwork_Types', create 4 subtypes under Artwork parent:

  - 5.1- 'Record' (related class: 'Record').

  - 5.2- 'Unit' (related class: 'Unit').

  - 5.3- 'Material' (related class: 'Material').

  - 5.4- 'Non-material' (related class: 'Nonmaterial').

- 6- Inside 'Space_Types', create 2 subtypes under Space parent:

  - 6.1- 'Region' (related class: 'Region').

  - 6.2- 'Address' (related class: 'Address').

- 7- Inside 'Record_Types', create 3 starting rows (nowadays related to 3 django classes/models):

  - 7.1- 'Account Ces' (related class: 'AccountCes')

  - 7.2- 'Account Bank' (related class: 'AccountBank')

  - 7.3- 'Unit Ratio'(related class: 'UnitRatio')

- 8- At this point, we can exclude some admin menu items/views, editing the admin.py inside General app/folder and commenting some lines at the bottom of that file (these lines have a comment marking which ones and some info):

  - 8.1- Comment the line 'admin.site.register(Being_Type, MPTTModelAdmin)'.

  - 8.2- Comment the line 'admin.site.register(Art, MPTTModelAdmin)'.

  - 8.3- Comment the line 'admin.site.register(Artwork_Type, MPTTModelAdmin)'.

  - 8.4- Comment the line 'admin.site.register(Space_Type, MPTTModelAdmin)'.

  - 8.5- If you don't want to edit directly the whole Types tree, comment the line 'admin.site.register(Type, MPTTModelAdmin)' and perhaps also the Concept main tree (commenting the line 'admin.site.register(Concept, MPTTModelAdmin)').

- 9- Now we can start defining some production subtypes for each main subclasses, using the appropiate '*_Types' view, and assigning the correct parent for each one (for example: inside Unit_Types you can put 'Currency' and then 'Social currency', 'Fiat currency' and 'Cryptocurrency', all under type Currency).

- 10- Also we can start defining Arts (they are all Verbs), as Jobs or Relation kinds, which can be nested.

- 11- Also we can start defining real items of each type: some Projects, some Persons (which can be related eachother), some currency Units, some Regions (which can be nested), some Addresses or Accounts (which can be assigned to a person or project), etc.



'General' FAQ's
-----

- **What is each of the general types for?**

  - Beings (abstact class) is for any kind of being or entity. Its Human real subclass generates uid's for any human type item. One day we may need to define other Being main types, non-human (say 'Animals').

  - Arts (real class, as a tree) is for all relations, activities, jobs, actions, etc... All them are Verbs, defined as so with the 'name' version, the verb 'infinitive' and the verb 'gerund'. All arts/verbs can be nested, they don't need a separate 'type', and we start defining them in two main trees: Relations and Jobs (sectors).

  - Spaces (abstract) is for any kind of data defining a physical space, zone or place. The two initial subclasses or types, generating real uid's for each item are Regions (which can be nested) and Addresses (which can be related to a Region).

  - Artworks (abstract) or simply Works, are for any thing created or produced by someone. They are always a result of an 'art' played by a 'being'. Main subclasses creating real whole tables and uid's are:

    - Units (medium table of units used, like currency, size, volume, etc),

    - Record (big table, which will hold unique id's for every record, divided in some record types: Accounts, Ratios, Memberships, etc),

    - Material (big table, holding unique id's for every physical thing, creation, product, etc),

    - Non-material (big table, holding uid's for every non-physical creation, say digital goods, cultural production, virtual products, etc).

  - Concepts (real class, as a tree) is for any item that is not a being, a verb, a place nor a created thing. All 'types' are concepts, and we can use other branches for other groups of concepts.


- **Why there are no 'types' for Arts and Concepts?**

Because arts are nestable and work like types, it's no required a kind of art because one art can be under another. Also concepts are nestable and the 'types of things' are just one branch of Concepts.


- **When we need to define a new kind of Record?**

The Record table is used to hold and give a uid to every unique record, which can be of any record_type. This way we have no possible conflicts between unique registered records (mainly digital). A record can hold, separately as a unique item, the relation between a person and a project (like oficial memberships), can have a creation date (and history), a related physical document, a related place or art, etc. It depends on the kind of record we need. We will define a new record type to hold all the contracts, the insurances, the licences, etc. They are already defined as records the accounts and the inter-units ratios.
