{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "colab_type": "text",
    "id": "HvmQXkErd8Po"
   },
   "source": [
    "<center>\n",
    "     <img src=\"https://images.idgesg.net/images/article/2019/07/cso_nw_cryptojacking_hacker_by_kentoh_gettyimages-1008725032_cryptocurrency_bitcons_by_thaimynguyen_gettyimages-954471176_abstract_globe_targeted_systems_by_blackdovfx_gettyimages-10295345000_2400x1600-100805352-large.jpg\" width='60%'> \n",
    "</center>\n",
    "\n",
    "----\n",
    "<h1 style=\"text-align: center\"><font size='8'><code style=\"background:black;color:white\">Smart Trading: Bitcoin Price Prediction</code></font></h1>\n",
    "<h2 style=\"text-align: center\"><font size='4'><code style=\"background:black;color:white\">By Saud Ishaq</code></font></h2>\n",
    "<h3 style=\"text-align: center\"><font size='4'><code style=\"background:black;color:white\">August 2020</code></font></h3>\n",
    "\n",
    "<br><center>\n",
    "<body style=\"text-align: center\"> <font size= '1.5'>This notebook is submitted as part of the requirements to pass Data Science Diploma program by <a href=\"https://weclouddata.com/\">\"We Cloud Data\"</a>, located in Toronto, Ontario, Canada</font></body>\n",
    "</center>\n",
    "\n",
    "--------"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "colab_type": "text",
    "id": "h7hvVIjpd8Pp"
   },
   "source": [
    "# Introduction"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Financial industry is one of the top industries relying heavily on Artificial Intelligence (AI) for their day-to-day operations.  New technologies and development in the AI sector influence the performance of financial institutions directly.  For example, car insurance companies can now use AI to estimate the actual driving behaviour of clients and determine the risk associated with their driving based on speed and GPS tracking devices that did not exist or were not accessible a decade ago. This allows the company to set insurance rates that are personalized to each client and provide them with more accurate indicators that can be used in their actuarial evaluations to have a better future position in the face of increasing claims and ultimately avoid future deficits.  Car insurance is just one service offered in the pool of financial services sector, and tracking technology is not the only modern technology available and accessible one.  Due to many technological advancements and cloud service, many services became more powerful than ever.  With access to millions of data sources and the use of Data Science, financial industry can now offer dynamic services with more personalization with the help of AI tools.\n",
    "\n",
    "Understanding clients and targeting the right customers helps the industry to grow.  Nonetheless, this research is focusing on the investment sector.  The use of technology and Data Science in this field is more concerned about finding patterns and predicting prices based on thorough analysis of the target market.  This advanced type of AI application is not as established as the simple use cases, such as the car insurance example.  Investment decisions need to be based on many factors, where AI tools can help with.  There has been an emergence of trading bots, where APIs are used from some websites and incorporated into codes that allows a person to have predetermined set of commands and criteria for when to buy or sell a commodity.  This type of AI is advanced, however, even bots can get confused in new situations that they were not trained on.  \n",
    "\n",
    "When it comes to trading commodities, trading bots can detect patterns in the past and predict a specific behavior, then leverage that knowledge of the predicted outcome to maximize trading gains.  However, the market is highly speculative, and other factors can play a role in price changes, such as news related to the commodity or news about competitors, economical situations, political situations, natural disasters, social trends, greed, and fear indicators.  Of course, a highly efficient trading bots should have access to all indicators that play a role in moving market prices. Does that mean that anyone can have accurate predictions if they combine all of that in a trading bot?  Even though the technology has advanced a lot in the past few years, combining all this data in one model could be hard as they need to be represented in numerical form for the model to be able to run mathematical calculations on them and find the hidden patterns, as well as many parameters, and hyper parameters must be set and evaluated to find the best model.  This process could take a long time and requires strong computing power. \n",
    "\n",
    "\n",
    "**<center>Model Objectives: Predict a Cryptocurrency Closing Price</center>**\n",
    "\n",
    "<a href=\"https://en.wikipedia.org/wiki/Bitcoin\">Bitcoin</a> was invented in 2008 by an unknown person or group of people using the name Satoshi Nakamoto. It is a decentralized digital currency without a central bank or single administrator that can be sent from user to user on the peer-to-peer bitcoin network without the need for intermediaries.\n",
    "    \n",
    "Over the years Bitcoin has grown in popularity and in risk reputation as it has shown high volatility compared to stocks and other financial commodities with 2017 being it's highest peak in value. With the increased demand for using digital currencies and the various solutions offered on the blockchain along with many stable coins, businesses and financial institutions were able to see the value this type of currency can add to their wealth and how much it can lower their costs.  Bitcoin specifically does not have many applications in the real world, besides its use as an asset with value that can be used for payments.  \n",
    "After the COVID_19 pandemic and the travel ban all over the world, many people realized the need for using fast and affordable means to transfer funds and to store their wealth in a decentralized asset that is not directly affected by a specific country's economy.  Many countries have stated that they are looking into digital currencies and believe that it could be beneficial for their country.  In April 2020, <a href=\"https://www.economist.com/finance-and-economics/2020/04/23/china-aims-to-launch-the-worlds-first-official-digital-currency\">China was the leading</a> and only country that issued their own digital currency and started initial testing with its four largest banks.  While other countries like the United States of America are still only using fiat currency. In a recent statement by the federal court, <a href=\"https://news.bloomberglaw.com/us-law-week/bitcoin-deemed-money-under-d-c-financial-services-law\">Bitcoin</a> is now considered money.  This has a great impact on the perceived value of Bitcoin.  After the announcement, the price went higher and the crypto currency market is in its first bull run since 2017.\n",
    "\n",
    "The target prediction is to predict the next price point.  While uncertainty and volatility are part of the crypto fame, a successful model should show a general direction of the price movement.\n",
    "For the use cases of AI for investment decisions, this notebook will demonstrate how to build a model to predict the price movement direction of a commodity. Furthermore, it provides a separate visualization dashboard that analyzes the dataset obtained to show a deeper analysis of the price movement and the correlation to other features such as number of trade orders, or day of the week.  \n",
    "\n",
    "**Note** <br>\n",
    "This notebook is one part of a research paper that is not finalized yet.  The paper aims to demonstrate several use cases of AI and simplify them to show their benefits and the obstacles that might be faced when used in the financial industry.  The paper will be focusing on theoretical aspects of financial technologies.  Among many related topics, it will dive into the world of digital currencies to show their impact on the existing financial industry practices, including Swift Plans and incorporating blockchain oracles in their programs.\n",
    "\n",
    "Kindly note that most of the proceeding qualitative Data is from the writer's accumulated knowledge and experience throughout the studying period of Data Science and involvement in cryptocurrency trading. Quantitative data is collected using API from an unofficial version of Binance Client.  Recommended readings for topics related to this notebook will be listed in the **Resources** section at the end."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "heading_collapsed": true
   },
   "source": [
    "## Conclusion"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "hidden": true
   },
   "source": [
    "The cryptocurrency market is highly volatile, and the training set fell in the period where Bitcoin was dumped to $3000 levels after the investors wanted to liquidate their assets to reduce their risks.  The final prediction of the model did not offer an accurate result and the mean square error is high, while the predicted pattern looks like it is following a somewhat correct pattern compared to actual values, it is still risky to use it in decision making due to Bitcoin's inherited volatility. This could be due to the validation set being in period that is caused by unexpected factor, a \"global pandemic\".   \n",
    "The model must be tuned further, or the selection of model could be changed.  To get a better prediction, more features could be added, including days of the week, sentiment analysis, search trend, and gold index.  Further research will be done to select the right features and the sources to get them.  Another approach would be to use the model for a more macro prediction of the price instead of the current model that predicts short term.\n",
   ]
  }
