# Evostab_forestplot
Potential beginning of a evostab forest plot
#loading library needed
library(ggplot2)
library(ggsci)
library(ggthemes)


# following naming conventions for the csv.file 
Fluxxer_psuedo_data<-read.csv('fluxxerdata')


# the csv file fluxxer_psuedo_data is called
ggplot(Fluxxer_psuedo_data, aes(x = y, y = x)) +
  
  # determining the shape, size, and group by for the dataset.
  # there will be a line present to take care of NA values in the future 
  
  # in addition the fluxxer script CIs will be taken into consideration as well. 
  geom_pointrange(
    aes(xmin = ymin, xmax = ymax, color = group, shape = shape),
    size = 1.2, fatten = 1, fill = "gray70", alpha = 0.5
  ) +
  
  geom_segment(
    aes(x = ymin, xend = ymin, y = x - 0.1, yend = x + 0.1), color = "black"
  ) +
  geom_segment(
    aes(x = ymax, xend = ymax, y = x - 0.1, yend = x + 0.1), color = "black"
  ) +
  
  # labelling the titles and x and y axises. 
  labs(
    x = "Mutation Rate (mu)",
    y = "",
    colour = "Group",
    shape = "Shape",
    title = "Mutation Rate for Sequences"
  ) +
  
  # background theme and colors 
  #in the future, theme_evostab() will be used 
  scale_color_npg() +
  scale_shape_manual(values = c("circle", "triangle")) +
  +
  theme(
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    panel.background = element_rect(fill = "gray90", colour = "black"),
    panel.border = element_rect(fill = NA, color = "black"),
    legend.background = element_rect(fill = "white", colour = "black"),
    legend.key = element_blank()
  )

# when completed all the user will use is the call forestplot(). However function has not been created as of yet.
