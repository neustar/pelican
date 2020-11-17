# PeLICAn: Private Learning and Inference for Causal Attribution

## DEFINING ATTRIBUTION

Advertisers are interested in understanding and measuring the impact that campaigns have on consumer behavior. This information provides insight into consumer behavior and preferences, which can be interpreted and translated into tactical and strategic marketing actions.

To enable informed choices around advertising deployment, advertisers often seek to learn which of their previous approaches have proven to be effective. Effectiveness may be measured in terms of financial return on investment, cost per acquisition, or other metrics such as brand health.

Regardless of the method chosen for learning effectiveness,  the intention is to attribute "credit" for an outcome to all or parts of a "sequence" of advertising contacts that precede the outcome of interest (Neslin, 2009) and it involves determining "the partial value of each interactive marketing contact that contributed to a desired outcome" (Osur, 2012).

As an illustration, a set of 3 possible marketing contacts delivered to a particular entity might be represented by an ordered path of events **A**, **B** and **C**, where the subscript t refers to a particular point in time, with an outcome represented as **Y**:

<p style="text-align: center;"> <b>C<sub>t1</sub>, B<sub>t2</sub>, A<sub>t4</sub>, A<sub>t6</sub>, Y<sub>t7</sub>, C<sub>t9</sub></b> </p>

The term "sequence" is often used to refer to an ordered set of events associated with a particular entity, such as the path shown above. There is an implicit assumption that the entity against which the sequence is assembled represents a "user", but in practice it may be, for example, a first or third party cookie with incomplete purview of the user's event history. Identity graphs are often used to re-associate the events associated with various sub-entities back to a higher level "user" entity.

Attribution methodologies are broadly split into "rules-based" approaches and "learning" based approaches.

### RULES-BASED ATTRIBUTION

Here are some examples of how some commonly used industry rules-based approaches would be applied to the example sequence:

* **Last touch rule:** A<sub>t6</sub> gets 100% of the credit
* **First touch rule:** C<sub>t1</sub> gets 100% of the credit
* **Fractional rule:** each of C<sub>t1</sub>, B<sub>t2</sub>, A<sub>t4</sub>, A<sub>t6</sub> get 25% of the credit
* **Any touch rule:** C<sub>t1</sub> gets 100% of the credit, B<sub>t2</sub> gets 100% of the credit, A<sub>t4</sub>, A<sub>t6</sub> each get 50% of the credit

Singh et al. (Singh, 2018) have evaluated multiple attribution models applied to simulated data and concluded that simplistic methodologies such as last-click and first click are prone to higher overall error rates when compared to model-based approaches that are capable of learning probabilities of conversion from consumer journey data. 

An additional criticism of rules-based approaches is that even if advertisers can observe in a particular sequence that someone saw an ad and then bought the product, there is not necessarily a causal link between the two. It could be merely that the kind of person who was exposed to that form of advertising is also more likely to purchase the product (Tucker, 2012). This is the classic endogeneity problem of advertising - advertising not only affects demand, but also at least partly depends on demand (Berndt, 1991). Retargeting is a good example of this, where someone who has visited a particular advertiser's website already receives additional ads for that advertiser after the visit.

### BEYOND RULES-BASED ATTRIBUTION

To overcome the limitations of rules-based approaches, different types of "learning" based attribution methods have been developed, In what is commonly known in the industry as "Multi-touch Attribution", weights that determine the proportion of total credit that should be assigned to each of the marketing touches in a sequence are learnt from data. For example, in the simplest case the impacts of the different marketing touches on Y can be learnt by calibrating the weights **w<sub>1-4</sub>** using a linear regression representation such as

<p style="text-align: center;"> <b>Y = w<sub>0</sub> + w<sub>1</sub> * C<sub>t1</sub> + w<sub>2</sub> * B<sub>t2</sub> + w<sub>3</sub> * A<sub>t4</sub> + w<sub>4</sub> * A<sub>t6</sub></b> </p>

In practice linear regression models are not commonly used, and work has been done on logistic regression approaches (Dalessandro, 2012) and many other model forms. While rules-based approaches operate on converting outcomes only, learning approaches need to consider both converting and non-converting paths to calculate the individual weights that determine the overall probability of conversion across different paths.

### ACCURATE ATTRIBUTION

Multiple studies from Google and others conclude that the most accurate forms of attribution currently available incorporate a learning mechanism and also account for causality. Causal measurement makes it possible to say how effective advertising is at changing user behavior. (Singh, 2018). Operationalizing causal measurement in practice requires not only measuring marketing's impact on a consumer's decision to purchase, but also quantifying the consumer's inherent propensity to convert (Kelly, 2018).

## IMPLICATIONS OF REMOVING ACCURATE MEASUREMENT

Advertisers choose among the set of attribution models available to them and their chosen attribution model provides a lens through which they perceive the efficiency of different marketing tactics. This lens informs their spend allocation choices.

Altering the choice of attribution methods available to advertisers will likely have an impact in the following ways:

1. **Advertisers may experience diminished confidence in their ability to measure the impact of digital marketing accurately and this may lead to lower spend in digital channels overall.** The overall share of advertising spend currently allocated to digital marketing is underpinned by advertisers' belief that they are able to accurately measure its ongoing performance, both within the digital ecosystem and relative to the performance of non-digital channels. Without the means to accurately measure and validate the success of ads, investment in digital marketing could diminish significantly as advertisers move spend to accurately measurable channels (Ravichandran, 2019). This reallocation of marketing investment away from digital is expected to disproportionally impact smaller publishers who do not have the ability to leverage large amounts of first party data about their users.
1. **A change in perception of tactic efficiency will create winners and losers in the ad-tech ecosystem.** For those advertisers who choose to continue spending in digital channels the spend allocations they make may be altered radically their new lens on effectiveness is wholly determined by the attribution methods that would be available. This has the potential to create winners and losers in the ad-tech industry. As Google (Singh, 2018) notes, the measurement approach chosen can have a significant impact on the advertiser's perception of the relative performance efficiency of different channels and creatives Singh et al  (Singh, 2018) demonstrated that different media channels are impacted in different ways by the inaccuracies of simplistic attribution methods, which creates the potential for unfair crediting within the ads ecosystem. 
1. **The ad market overall will become less efficient and these inefficiencies will impact advertisers and consumers.** Without access to accurate attribution, those advertisers who choose to continue spending in digital channels will be forced to allocate their spend less efficiently, since less accurate attribution leads directly to reduced knowledge about efficiency and therefore less cost-effective spending. This wasteful spending may result in higher customer acquisition costs for advertisers, and may in turn be passed on to consumers in the form of higher prices.

## WHAT MIGHT BE REQUIRED TO SUPPORT ACCURATE ATTRIBUTION?

* **Complete browser interaction pathways that include marketing originating from multiple channels and vendors, as well as organic signals from brand interactions.**  
MTA measurement requires visibility of marketing delivered to users across multiple domains and from multiple vendors online. The current proposed Conversion Measurement API, in both the event-level and the aggregated forms, partitions measurement through reporting origins. In practice, multiple campaigns from different vendors and channels may impact a particular set of conversions and the interplay between these marketing activities is important to properly measure marketing impact.  
The combination of signals from multiple sources into browser-based sequences would conform to the same privacy guarantees associated to the current Conversion Measurement API proposals, since the more complete sequence information would be subject to the same lower bounds on levels of aggregation and differential privacy mechanisms prior to reporting.  
The collection of such data at the entity level mirrors the way in which the FLoC proposal intends to leverage site visitation data at the browser-level, and can be implemented with a similar security model.
* **Observation of consumer pathways that include both converting and non-converting sequences of events.** 
Learning-based MTA approaches are differentiated in that they allow not only for the measurement of marketing impact on conversions, but also for measuring the impact of organic user behaviour patterns and general user characteristics on the probability that a conversion will occur. To build such models, it is necessary to utilize information about user histories of organic behaviour and marketing interactions for both successful and unsuccessful user paths.  
The current conversion measurement proposals only cover the functionality of reporting on characteristics of user paths that resulted in conversions, which is insufficient for the estimation of conversion models.  
A possible solution is the extension of the current proposed APIs to allow for browsers to collect and report marketing and organic activities without the need for a conversion trigger. Such data would be subject to the same privacy preserving mechanisms currently proposed for conversion-based measurement, such as minimum levels of aggregation and the application of differential privacy mechanisms to reported results.
* **Grouping of sequence elements and feature generation with respect to each entity.**  
A learning-based MTA approach requires the ability to consolidate all elements in a sequence of collected events into a set of features associated with a unique entity, and to encode these elements into a numerical representation that is compatible with a chosen modelling approach. In addition, there would be the need for entity coordination for the purpose of model estimation.  
This coordination can be achieved through a Federated Learning strategy or through the collection of sequences in a protected environment such as the proposed Helper Servers. In either case, privacy guarantees around this coordination process would be inherited from the proposals it leverages.
* **Model training and sensitivity analysis.**  
The process of secure and private model training either through federation or though centralization within the helper servers is needed for the generation of MTA models. For this purpose, the system would need to be able to accept general algorithms from a reporting origin (ad-tech company) that would instruct the helpers or browsers on how to process sequence data into a numerical form suitable for model estimation.  
In addition to model generation and training, the resulting models would need to be evaluated onto each observed conversion for the purpose of attribution generation. This process is akin to performing a sensitivity analysis on inputs to each observation in order to determine attribution to multiple marketing events that preceded a conversion.  
The resulting attribution values would then be aggregated and obfuscated by the helper servers towards a desirable level of enforcement of privacy guarantees before these aggregated reports would be sent to the reporting origin.


## BIBLIOGRAPHY

* Berndt, E. R. 1991. The practice of econometrics: Classical and contemporary. Reading, Mass.: Addison-Wesley Publishing.
* Dalessandro, B., Perlich, C., Stitelman, O., Provost., F. 2012. "Causally motivated attribution for online advertising." Proceedings of the Sixth International Workshop on Data Mining for Online Advertising and Internet Economy. http://doi.acm.org/10.1145/2351356.2351363. 7:1-7:9.
* Ravichandran, D., Korula, N. 2019. "Effect of disabling third-party cookies on publisher revenue." https://services.google.com/fh/files/misc/disabling_third-party_cookies_publisher_revenue.pdf.
* Kelly, J., Vaver, J., Koehler, J. 2018. "A Causal Framework for Digital Attribution." https://research.google/pubs/pub46905/.
* Singh, K., Vaver, J., Little, R., Fan, R. 2018. "Attribution Model Evaluation." https://research.google/pubs/pub46901/.
* Neslin, S.A, Shankar, V. 2009. "Key issues in multichannel customer management: current knowledge and future directions." Journal of Interactive Marketing 23 (1): 70-81.
* Osur, A., Riley, E., Moffett, T., Glass, S., Komar, E. 2012. The Forrester Wave Interactive Attribution Vendors Q2 2012. Forrester White Paper.
* Tucker, C. 2012. "The Implications of Improved Attribution and Measurability for Antitrust and Privacy in Online Advertising Markets." Geo. Mason L. Rev (Geo. Mason L. Rev. 20) 1025.
