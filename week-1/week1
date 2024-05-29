import streamlit as st
import numpy as np
import pandas as pd

def learn(concepts, target):
    '''
    learn() function implements the learning method of the Candidate elimination algorithm.
    Arguments:
        concepts - a data frame with all the features
        target - a data frame with corresponding output values
    '''
    # Initialise S0 with the first instance from concepts
    specific_h = concepts[0].copy()
    general_h = [["?" for _ in range(len(specific_h))] for _ in range(len(specific_h))]

    # The learning iterations
    for i, h in enumerate(concepts):
        # Checking if the hypothesis has a positive target
        if target[i] == "Yes":
            for x in range(len(specific_h)):
                # Change values in S & G only if values change
                if h[x] != specific_h[x]:
                    specific_h[x] = '?'
                    general_h[x][x] = '?'

        # Checking if the hypothesis has a positive target
        if target[i] == "No":
            for x in range(len(specific_h)):
                # For negative hypothesis change values only in G
                if h[x] != specific_h[x]:
                    general_h[x][x] = specific_h[x]
                else:
                    general_h[x][x] = '?'

    # find indices where we have empty rows, meaning those that are unchanged
    indices = [i for i, val in enumerate(general_h) if val == ['?', '?', '?', '?', '?', '?']]
    for i in indices:
        # remove those rows from general_h
        general_h.remove(['?', '?', '?', '?', '?', '?'])
    # Return final values
    return specific_h, general_h

# Streamlit UI
st.title('Candidate Elimination Algorithm')

# File uploader widget for users to upload their dataset
st.sidebar.title('Upload Dataset')
uploaded_file = st.sidebar.file_uploader("Upload CSV", type=["csv"])

if uploaded_file is not None:
    # Load data
    data = pd.read_csv(uploaded_file)

    # Displaying uploaded data
    st.subheader('Uploaded Dataset')
    st.write(data)

    # Separating concept features from Target
    concepts = np.array(data.iloc[:,0:-1])
    target = np.array(data.iloc[:,-1])

    # Run the learning algorithm
    specific_h, general_h = learn(concepts, target)

    st.subheader('Initial Hypothesis')
    st.write('Specific_h:', specific_h)
    st.write('General_h:', general_h)

    st.subheader('Steps of Candidate Elimination Algorithm')

    # Displaying steps
    for i, (s, g) in enumerate(zip(specific_h, general_h), start=1):
        st.write(f"Step {i}")
        st.write('Specific_h:', s)
        st.write('General_h:', g)
        st.write('------------------------')

    st.subheader('Final Hypotheses')
    st.write('Final Specific_h:', specific_h)
    st.write('Final General_h:', general_h)
