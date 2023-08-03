In an experiment to investigate the Stroop effect, a group of students were timed reading out 25 randomly ordered color names, first in black ink and then in a color other than the one they name (e.g. the word “red” in blue ink). The results are presented in the text file [stroop.txt](https://scipython.com/static/media/2/examples/E6/stroop.txt). Missing data are indicated by the character X.

Analyze the data from a Stroop effect experiment (obtain the mean and (standard deviation ) times per word (sec)).

My Solution with comments are shown below. I have used Google Colab to execute the code.
#### Solution: 
````python
#stroop data
#There is no column separator

import numpy as np
# Read in the data from stroop.txt, identifying missing values and
# replacing them with NaN (missing values are represented by X)

data = np.genfromtxt('stroop.txt', skip_header=1,
                     dtype=[('student','u8'), ('gender','S1'), ('black','f8'), ('colour','f8')], delimiter=',', missing_values='X')


#students read out 25 randomly ordered colour names
nwords = 25

# Remove invalid rows from data set
filtered_data = data[np.isfinite(data['black']) & np.isfinite(data['colour'])]


# Extract rows by gender (M/F) and word colour (black/colour) and normalize
# to time taken per word
fb = filtered_data['black'][filtered_data['gender']==b'F'] / nwords     #black words read by female/nwords
mb = filtered_data['black'][filtered_data['gender']==b'M']  / nwords    #black words read by male/ nwords
fc = filtered_data['colour'][filtered_data['gender']==b'F'] / nwords
mc = filtered_data['colour'][filtered_data['gender']==b'M'] / nwords

# Produce statistics: mean and standard deviation by gender and word colour
mu_fb, sig_fb = np.mean(fb), np.std(fb)
mu_fc, sig_fc = np.mean(fc), np.std(fc)
mu_mb, sig_mb = np.mean(mb), np.std(mb)
mu_mc, sig_mc = np.mean(mc), np.std(mc)


print('Mean and (standard deviation) times per word (sec)')
print('gender |    black      |    colour     | difference')
print('   F   | {:4.3f} ({:4.3f}) | {:4.3f} ({:4.3f}) |   {:4.3f}'
                    .format(mu_fb, sig_fb, mu_fc, sig_fc, mu_fc - mu_fb))
print('   M   | {:4.3f} ({:4.3f}) | {:4.3f} ({:4.3f}) |   {:4.3f}'
                    .format(mu_mb, sig_mb, mu_mc, sig_mc, mu_mc - mu_mb))
`````