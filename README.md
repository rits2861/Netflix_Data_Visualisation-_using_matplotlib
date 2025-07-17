# Netflix_Data_Visualisation-_using_matplotlib

#importing libraries
import pandas as pd
import matplotlib.pyplot as plt

#loading data
df=pd.read_csv(r"C:\Users\RITIKA SHARMA\Desktop\Matplotlb\Netflix_matplotlib project New.csv")
print(df.head)

# clean data
df=df.dropna(subset=["type","title","director","cast","country","date_added","release_year","rating","duration","listed_in","description"])

type_counts=df['type'].value_counts()
plt.figure(figsize=(6,4))
plt.bar(type_counts.index, type_counts.values,color=['skyblue',"orange"])
plt.title("Number of Movies vs TV Shows on Netflix")
plt.xlabel("Type")
plt.ylabel("Count")
plt.tight_layout()
plt.savefig("MoviesVsTvShows.png")
plt.show()


rating_counts=df["rating"].value_counts()
plt.figure(figsize=(8,6))
plt.pie(rating_counts,labels=rating_counts.index,autopct="%1.1f%%", startangle=90)
plt.title("Percentage of Ratings")
plt.tight_layout()
plt.savefig("RatingsMoviesVsTvShows.png")
plt.show()

movie_df=df[df["type"]=="Movie"].copy()
movie_df["duration_int"]=movie_df["duration"].str.replace("min","").astype(int)
plt.figure(figsize=(8,6))
plt.hist(movie_df["duration_int"],bins=30,color="purple",edgecolor="Black")
plt.title("Movie Distribution")
plt.xlabel("Duration Minutes")
plt.ylabel("No. of Movies")
plt.tight_layout()
plt.savefig("MoviesDurationhists.png")
plt.show()

release_counts=df["release_year"].value_counts().sort_index()
plt.figure(figsize=(10,6))
plt.scatter(release_counts.index, release_counts.values, color="red")
plt.title("Release year vs  no of Shows")
plt.xlabel("Release year ")
plt.ylabel("No. of Shows")
plt.tight_layout()
plt.savefig("Release_year _scatter.png")
plt.show()


country_counts=df["country"].value_counts().head(10)
plt.figure(figsize=(8,6))
plt.barh(country_counts.index,country_counts.values,color="green")
plt.title("Top 10Countries by NO. of Shows")
plt.xlabel("No. of Shows")
plt.ylabel("Country")
plt.tight_layout()
plt.savefig("top10Country.png")
plt.show()

content_by_year=df.groupby(['release_year',"type"]).size().unstack().fillna(0)

fig, ax=plt.subplots(1,2,figsize=(12,5))
#first subplot
ax[0].plot(content_by_year.index,content_by_year["Movie"],color="Blue")
ax[0].set_title("Movies released per year")
ax[0].set_xlabel("year")
ax[0].set_ylabel("Number of Movies")
#second
ax[0].plot(content_by_year.index,content_by_year["TV Show"],color="Orange")
ax[0].set_title("TV Show released per year")
ax[0].set_xlabel("year")
ax[0].set_ylabel("Number of TV Shows")

fig.suptitle("Comparison of Movies and TV Shows")


plt.tight_layout()
plt.savefig("Movies_VStvshows.png")
plt.show()
