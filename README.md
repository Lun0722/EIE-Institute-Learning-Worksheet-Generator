
import streamlit as st
from random import sample, choice

# ---------------------
# 設定 Streamlit 頁面
# ---------------------
st.set_page_config(page_title="EIE Institute Demo Worksheet", layout="centered")
st.title("📚 EIE Institute Demo Worksheet Generator")

# ---------------------
# 老師輸入文章或連結
# ---------------------
article = st.text_area("Enter article text or paste a link here:", height=150)

# ---------------------
# 選程度
# ---------------------
level = st.selectbox(
    "Select English Level:",
    ["Basic", "Intermediate", "Advanced"]
)

# ---------------------
# 選字數級距
# ---------------------
word_count_ranges = {
    "Basic": "350–400 words",
    "Intermediate": "400–550 words",
    "Advanced": "550+ words"
}
st.markdown(f"**Recommended Word Count:** {word_count_ranges[level]}")

# ---------------------
# 模擬生成學習單
# ---------------------
def generate_demo_worksheet(text, level):
    # 模擬主要單字與片語
    demo_vocab = {
        "Basic": ["economy", "money", "work", "school", "people", "city", "time", "day", "food", "help"],
        "Intermediate": ["GDP", "inflation", "policy", "employment", "environment", "investment", "trade", "market", "finance", "growth"],
        "Advanced": ["fiscal tightening", "monetary policy", "supply chain", "geopolitics", "sustainability", "macroeconomics", "capital allocation", "regulation", "quantitative easing", "productivity"]
    }
    vocab = sample(demo_vocab[level], k=5)  # 取5個單字

    # 模擬暖場問題
    warmup = {
        "Basic": ["What is your favorite hobby?", "Do you like reading?", "What did you eat today?"],
        "Intermediate": ["How does the economy affect daily life?", "What are your career goals?", "Describe a recent news article you read."],
        "Advanced": ["What are the implications of fiscal policy on global markets?", "How does inflation impact investment decisions?", "Discuss sustainability challenges in modern economies."]
    }
    warmup_q = sample(warmup[level], k=3)

    # 模擬討論問題
    discussion = {
        "Basic": ["Why is work important?", "How do people help each other?", "What do you like about your city?"],
        "Intermediate": ["How does trade affect your country?", "What policies can improve employment?", "Why is investment important?"],
        "Advanced": ["Analyze the impact of quantitative easing on the stock market.", "Evaluate the role of regulation in financial systems.", "Discuss the effects of geopolitics on international trade."]
    }
    discussion_q = sample(discussion[level], k=3)

    # 組成學習單
    worksheet = f"### Key Vocabulary & Phrases:\n- " + "\n- ".join(vocab)
    worksheet += "\n\n### Warm-up Questions:\n- " + "\n- ".join(warmup_q)
    worksheet += "\n\n### Discussion Questions:\n- " + "\n- ".join(discussion_q)

    return worksheet

if st.button("Generate Demo Worksheet"):
    if not article.strip():
        st.warning("Please enter some text or link first.")
    else:
        demo_output = generate_demo_worksheet(article, level)
        st.success("Demo worksheet generated! 🎉")
        st.markdown(demo_output)

        # 可下載為文字檔
        st.download_button(
            label="⬇️ Download Worksheet (TXT)",
            data=demo_output,
            file_name="demo_worksheet.txt",
            mime="text/plain"
        )
