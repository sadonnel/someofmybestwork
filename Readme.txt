Project Part 1 colley matrix (short way)

# importing data 
load("/Users/SamDonnelly/Documents/R Data Sets/ncaaf_2010.rdata")

# creating the vector b where the ith element is 
# 1+.5(team i num wins - team i num losses)
vector.b = 1 + .5*(df$wins - df$losses)

# computing total games played per team
n.tot = df$wins + df$losses

# creating the matrix
# setting up a matrix of zeros
m = matrix(data = 0, nrow = 120, ncol = 120)

# filling the matrix with -1*(# games team i played team j
for(i in 1:120){
  for(k in df$opponents[[i]]){
    m[i,k] = m[i,k] - 1
  }
}

# filling in the diagonal
diag(m) = 2 + n.tot

# solving for ranks
ranks = solve(m, vector.b)

solution = data.frame(df$teams,ranks)

solution[order(ranks,decreasing = T),]
