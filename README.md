import streamlit as st
import time
import random

# Page Config
st.set_page_config(page_title="TerraBound Digital Twin", page_icon="🌱")

st.title("🌱 TerraBound: Digital Twin AI")
st.markdown("### *Mission Control for Biodiversity Restoration*")

# Sidebar for IoT Inputs
st.sidebar.header("📡 Live IoT Sensor Feed")
temp = st.sidebar.slider("Ambient Temperature (°C)", 15, 50, 25)
moisture = st.sidebar.slider("Soil Moisture (%)", 0, 100, 40)
uv_index = st.sidebar.sidebar.number_input("UV Index", 0, 15, 5)

# Main Interface
species = st.selectbox("Select Species for Simulation", 
                      ["Acacia tortilis (Umbrella Thorn)", 
                       "Olea europaea (Wild Olive)", 
                       "Kigelia africana (Sausage Tree)"])

is_hardened = st.toggle("Enable CRISPR Genetic Hardening")

if st.button("Run Digital Twin Simulation"):
    with st.status("Analyzing Genetic Resilience...", expanded=True) as status:
        st.write("Syncing with Subterranean Cryo-Vault...")
        time.sleep(1)
        st.write("Running Trophic Cascade Models...")
        time.sleep(1)
        st.write("Simulating 2050 Climate Stressors...")
        time.sleep(1)
        status.update(label="Simulation Complete!", state="complete", expanded=False)

    # Logic for Prediction
    if is_hardened:
        survival = random.randint(88, 99)
        st.success(f"PROJECTION: {survival}% Survival Rate")
        st.balloons()
    else:
        survival = random.randint(15, 45)
        st.error(f"PROJECTION: {survival}% Survival Rate (High Risk of Extinction)")

    st.metric(label="Biomass Growth Acceleration", value="40%", delta="Aeroponics Active")
    st.progress(survival, text="Species Resilience Level")
