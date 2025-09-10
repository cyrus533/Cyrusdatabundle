const fetch = require("node-fetch");

module.exports = async (req, res) => {
  if (req.method !== "POST") {
    return res.status(405).json({ error: "Method not allowed" });
  }

  try {
    const { name, network, bundle, number } = req.body;

    if (!name || !network || !bundle || !number) {
      return res.status(400).json({ error: "Missing fields" });
    }

    const message = `
📦 New Order
👤 Name: ${name}
📱 Number: ${number}
🌐 Network: ${network}
💰 Bundle: ${bundle}
    `;

    const response = await fetch(
      `https://api.telegram.org/bot${process.env.BOT_TOKEN}/sendMessage`,
      {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          chat_id: process.env.CHAT_ID,
          text: message,
        }),
      }
    );

    const data = await response.json();

    if (!data.ok) {
      throw new Error(data.description);
    }

    res.status(200).json({ success: true, message: "Order sent successfully!" });
  } catch (error) {
    console.error("Error:", error.message);
    res.status(500).json({ success: false, error: error.message });
  }
};
