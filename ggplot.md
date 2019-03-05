Untitled
================

``` r
data_cancer = read.csv("./data/cancer.csv") %>% 
  gather(key = factor, value = value, Binge_value:Obesity_value) %>% 
  separate(factor, into = c("factor", "1"), sep = "_") %>% 
  dplyr::select(-"1")

p =
  data_cancer %>% 
  ggplot(aes(x = value, y = Cancer_value)) +
  geom_point(aes(colour = factor ),
             alpha = 0.5) +
  labs(title = "{closest_state}",
       x = 'Factor Prevalence', 
       y = 'Cancer Prevalence',
       color = 'Factors') +
  theme_bw() + 
  theme(plot.title = element_text(size = 35, face = "bold"),
        axis.text=element_text(size=18),
        axis.title=element_text(size=18,face="bold")) +
  theme(legend.position = "bottom", legend.text=element_text(size=12),
        legend.title=element_text(size=15,face="bold")) +
  transition_states(factor, transition_length = 1, state_length = 3, wrap = TRUE) +
  enter_fade() +
  exit_fade()

gif = animate(p)
```
