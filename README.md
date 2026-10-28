# 🍟 Friterie Operations Analytics : Queuing & Inventory Optimization

### Executive Summary:

This project analyzes the operations of Friterie Riebedebie, a Belgian fries shop, across two areas: customer queuing and inventory management.
Using Python, a discrete-event simulation (SimPy) was built to model 100 days of customer arrivals, waiting times, lost customers and staff utilization, and an inventory model was used to classify products (ABC analysis), set optimal ordering policies (EOQ, safety stock, reorder level) at a 95% service level and compare two suppliers.
Findings show that a better spread of the same staff hours cuts waiting times and lost customers, and that switching the supplier of the best-selling snack lowers inventory costs by more than 20%. Based on these findings, I recommend the following actions:

1. Redistribute staff toward peak hours (lunch and evening) within the 18 man-hour limit.
2. Focus the product portfolio on high-revenue snacks and discontinue the lowest performers.
3. Switch the "Frikandel" supplier from VET to OLI to reduce total inventory costs.

#### Business Problem:

Friterie Riebedebie faces strong peaks in demand at lunchtime and in the evening. With a fixed staff schedule, customers wait too long during busy hours and some leave without ordering, while staff are under-used during quiet hours. On the supply side, the shop sells 10 snacks bought from two suppliers with different costs and lead times, without a clear inventory policy. This project explores how staffing, product portfolio and inventory decisions can be optimized to improve service quality and reduce costs.

#### Methodology:

1. Queuing Simulation: Built a discrete-event simulation in SimPy with a time-dependent number of servers (custom `VariableResource` class), hourly arrival rates, gamma-distributed service times and customer abandonment after 15 minutes, simulated over 100 days.
2. Queuing Analysis: Measured average and maximum waiting time, 95% waiting time quantile, % of lost customers and utilization per hourly time slot.
3. Staffing Optimization: Tested an alternative staffing schedule (more servers at 12:00, 17:00 and 18:00, fewer during off-peak slots) and compared it with the original schedule.
4. ABC Analysis: Estimated annual revenue per snack from customer preferences, prices and monthly traffic, then classified products into A / B / C categories with a Pareto chart.
5. Inventory Policy: Computed EOQ, safety stock and reorder level (continuous review) for the Frikandel and target stock levels (7-day periodic review) for the other 9 SKUs at a 95% service level, and simulated a full year of inventory using gamma-distributed demand and lead times.
6. Supplier Comparison: Compared the VET and OLI suppliers for the Frikandel on EOQ, safety stock, reorder level, inventory cost and material cost.

#### Skills:

1. Simulation Modeling: Discrete-event simulation with SimPy, including a custom resource with variable capacity.
2. Queuing Theory: Waiting times, abandonment, utilization and service level analysis.
3. Inventory Management: ABC analysis, EOQ, safety stock, reorder level, continuous vs periodic review policies.
4. Statistics & Probability: Gamma distributions for demand, lead and service times, quantiles and service levels.
5. Python Programming & Tools: Using Pandas, NumPy, SciPy, Matplotlib, Seaborn, SimPy and Jupyter Notebooks.

#### Results & Business Recommendation:

**Part A – Queuing management**

The original schedule did not match demand: waiting times and lost customers peaked at 13:00 and 18:00, while utilization dropped to about 35% in the first slot. Moving staff toward the peaks, while staying within the 18 man-hour limit, produced clear improvements:

| Metric | Original schedule | Optimized schedule |
|---|---|---|
| Staff per slot (10:00 → 20:00) | 2,2,3,1,1,1,1,2,2,2,2 | 1,2,3,1,1,1,1,3,3,1,1 |
| Average waiting time | 3.50 min | 2.10 min |
| 95% of customers wait less than | 13.5 min | 9.3 min |
| Lost customers | 2.9% | 0.8% |
| Average utilization | ~55–58% | ~59% |

**Part B – Inventory management**

The ABC analysis shows that 4 snacks (Frikandel, Mexican Specialty, Meat Skewer and Dutch Bitterballs) generate about 75% of revenue, while Dutch Bitterballs Veg, Shrimp Croquettes and Boulet bring in less than 10%.

With the current policy, total inventory costs reach €58,573 per year. Applying optimized parameters at a 95% service level lowers expected costs to €34,598. Switching the Frikandel supplier from VET to OLI brings further savings:

| Metric | VET | OLI | Difference |
|---|---|---|---|
| EOQ | 177 | 63 | -114 |
| Safety stock | 138 | 48 | -90 |
| Reorder level | 410 | 125 | -285 |
| Annual inventory cost (Frikandel) | €11,442.57 | €4,016.90 | -€7,425.67 |
| Total inventory cost (all products) | €34,598.18 | €27,172.51 | -21.46% |
| Material cost per unit | €0.40 | €0.43 | +7.5% |

I recommend these actions to improve service quality and cost performance:

1. Adopt the optimized staffing schedule and add flexible part-time staff during peaks.
2. Reduce peak pressure with self-service kiosks, mobile pre-ordering or an SMS queue system.
3. Promote Category A snacks (special editions, platters), bundle Category B snacks and discontinue Boulet and Shrimp Croquettes.
4. Use optimized EOQ, safety stock and target stock levels for every product.
5. Switch the Frikandel supplier to OLI (lower ordering cost, 2 vs 7 days lead time), for a net saving of about 14% after the higher material cost.

#### Next steps:

1. Collect real arrival and service time data to calibrate the simulation.
2. Test more staffing scenarios automatically with an optimization algorithm.
3. Include supplier quality and reliability in the supplier decision, not only cost.
4. Build a dashboard to monitor waiting times, stock levels and costs over time.

#### Files:

- `Operations analytics Friterie python file.ipynb` : Python code (simulation, ABC analysis, inventory model)
- `Friterie Riebedebie Report.pdf` : Final report

*Group project – Operations Analytics, EDHEC Business School.*
