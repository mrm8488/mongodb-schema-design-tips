![](https://thepracticaldev.s3.amazonaws.com/i/u7b9mvtin7rmhy4ohbut.JPG)

NoSQL databases are a relatively recent technology and so that there are a lot of questions about when and how to use them.

I have read a lot of articles that say something like: "if your data has relationships, don't use NoSQL". That's not true! It's like a fake mantra that I've read over and over again. In the most of scenarios we will have to model data with any kind of relationship and NoSQL databases are ready to deal with it. The key is how we model our data.

I am not saying NoSQL databases are the best option if you have *strongly related* data, but **having relationships in our data is not a sufficient argument to discard them.**

We will focus on MongoDB. One on the most popular NoSQL databases (document oriented). IMO, part of its success is due to its easy integration with popular JavaScript Back-End frameworks. Moreover, MongoDB is the *M* in the popular MEAN and MERN stacks.

Below, I will give you 5 quick but powerful rules to take into account on designing MongoDB's schemas (you can use them for similar databases too):


1. **As general rule, try to embed**  unless you have reasons not to do so.

2. **If the objects you are going to embed may be accessed in a isolated way** (it makes sense to access it out of the document context) **you have a reason for not embedding**.

3. **If the array with embedded objects may grow in an unbounded way, you have another reason for not embedding**. As a general rule, we should not embed more than a couple of hundreds of documents/objects neither more than a couple of thousands ObjectIDs.

4. **Denormalize** one or several fields of a document from the many side into the array in the one side (One-to-Many relationship) **can save us some extra queries** (application-level joins). IMO, denormalization is one of the keys to get the most out of this kind of databases. But, denormalization only makes sense if the denormalized field/s will be seldom updated. Otherwise, finding and updating all the instances is likely to overwhelm the savings that we get from denormalizing. So that, consider the read/write ratio for the field/s before denormalizing.

5. **Don't be afraid of application-level joins**. With the right indexing, they are barely more expensive than server-level joins.
(Update: last MongoDB versions includes the *$lookup* operator that allows us to do server-level JOINS, concretely LEFT OUTER JOINS).

And remember: **Design your schemas the way through fit as well as possible your application's data access patterns**. We want to structure our data to match the ways that our application queries and updates it.

If you want detailed information about how to model one-to-many and many-to-many relationships in MongoDB, check out my post: [MongoDB schema design patterns (I)](https://dev.to/mrm8488/mongodb-schema-design-patterns-i-4gdp)

[References](https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-3)
