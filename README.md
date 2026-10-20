# R-code-for-Lab-1load("~/.RData")
> # Absorbance vector 
> A <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> #Concentration vector
> C <- c(0.5, 1, 2, 4, 6, 8, 10)
> 
> # Now let's plot it
> # 2. Basic scatter plot
> plot(C, A, type = "l", col = "blue", lwd = 2, 
+      main = "Line Plot of Two Vectors", xlab = "X Axis", ylab = "Y Axis")
> 
> 
> 
> # 1. Define your individual data vectors
> C <- c(0.5, 1, 2, 4, 6, 8, 10)                        # Concentration (mM)
> A <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064) # Absorbance
> 
> # 2. Fit the linear regression model
> model <- lm(A ~ C)
> model_summary <- summary(model)
> 
> # 3. Calculate residuals and residual standard error (s_y/x)
> residuals_val <- residuals(model)
> s_yx <- model_summary$sigma  # Standard error of the regression
> 
> # 4. Create the scatter plot with adjusted y-limits for error bars
> plot(C, A, 
+      pch = 16, 
+      col = "blue", 
+      cex = 1.3,
+      ylim = c(0, max(A + s_yx) + 0.05),
+      main = "Individual Aspartame Calibration Curve", 
+      xlab = "Concentration (mM)", 
+      ylab = "Absorbance")
> 
> # 5. Add error bars representing regression residual error (± s_y/x)
> arrows(x0 = C, 
+        y0 = A - s_yx, 
+        x1 = C, 
+        y1 = A + s_yx, 
+        length = 0.05, 
+        angle = 90, 
+        code = 3, 
+        col = "darkblue", 
+        lwd = 1.2)
> 
> # 6. Add line of best fit
> abline(model, col = "red", lwd = 2)
> 
> # 7. Extract statistics for your lab report
> slope <- coef(model)["C"]
> se_slope <- model_summary$coefficients["C", "Std. Error"]
> r_squared <- model_summary$r.squared
> 
> # Convert slope and error to M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print values directly to Console
> cat("\n================ INDIVIDUAL LAB REPORT VALUES ================\n")

================ INDIVIDUAL LAB REPORT VALUES ================
> cat("Molar Absorptivity (mM^-1 cm^-1):", round(slope, 5), "\n")
Molar Absorptivity (mM^-1 cm^-1): 0.10328 
> cat("Molar Absorptivity (M^-1 cm^-1) :", round(molar_absorptivity_M, 2), "\n")
Molar Absorptivity (M^-1 cm^-1) : 103.28 
> cat("Std Error of Slope (M^-1 cm^-1) :", round(se_molar_absorptivity_M, 2), "\n")
Std Error of Slope (M^-1 cm^-1) : 4.45 
> cat("Std Error of Regression (s_y/x) :", round(s_yx, 5), "\n")
Std Error of Regression (s_y/x) : 0.03971 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.9908 
> cat("=============================================================\n")
=============================================================
> # 1. Define your individual data vectors
> C <- c(0.5, 1, 2, 4, 6, 8, 10)                        # Concentration (mM)
> A <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064) # Absorbance
> 
> # 2. Fit the linear regression model
> model <- lm(A ~ C)
> model_summary <- summary(model)
> 
> # 3. Extract regression coefficients & statistics
> intercept <- coef(model)["(Intercept)"]
> slope     <- coef(model)["C"]
> 
> se_slope  <- model_summary$coefficients["C", "Std. Error"]
> s_yx      <- model_summary$sigma  # Standard error of the linear regression
> r_squared <- model_summary$r.squared
> 
> # 4. Create the scatter plot
> plot(C, A, 
+      pch = 16, 
+      col = "blue", 
+      cex = 1.3,
+      ylim = c(0, max(A + s_yx) + 0.05),
+      main = "Individual Aspartame Calibration Curve", 
+      xlab = "Concentration (mM)", 
+      ylab = "Absorbance")
> 
> # 5. Add error bars representing regression residual error (± s_y/x)
> arrows(x0 = C, 
+        y0 = A - s_yx, 
+        x1 = C, 
+        y1 = A + s_yx, 
+        length = 0.05, 
+        angle = 90, 
+        code = 3, 
+        col = "darkblue", 
+        lwd = 1.2)
> 
> # 6. Add line of best fit
> abline(model, col = "red", lwd = 2)
> 
> # 7. Format line equation string and display on the plot legend
> eq_label <- sprintf("y = %.5fx + %.5f\nR² = %.4f", slope, intercept, r_squared)
> legend("topleft", 
+        legend = c("Data Points", "Line of Best Fit", eq_label), 
+        col = c("blue", "red", NA), 
+        pch = c(16, NA, NA), 
+        lty = c(NA, 1, NA), 
+        lwd = c(NA, 2, NA), 
+        bty = "n", 
+        cex = 0.9)
> 
> # 8. Convert Molar Absorptivity to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print formatted summary table to Console for lab report reporting
> cat("\n================ DAY 2 LAB REPORT OUTPUTS ================\n")

================ DAY 2 LAB REPORT OUTPUTS ================
> cat("Regression Equation              : y =", round(slope, 5), "* x +", round(intercept, 5), "\n")
Regression Equation              : y = 0.10328 * x + 0.07711 
> cat("Molar Absorptivity (ε)           :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε)           : 103.28 M^-1 cm^-1
> cat("Std Error in Molar Absorptivity  :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in Molar Absorptivity  : 4.45 M^-1 cm^-1
> cat("Std Error of Linear Regression   :", round(s_yx, 5), "\n")
Std Error of Linear Regression   : 0.03971 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.9908 
> cat("===========================================================\n")
===========================================================
> # 1. Standard concentrations (7 unique levels in mM)
> C_single <- c(0.5, 1, 2, 4, 6, 8, 10)
> 
> # 2. Pooled absorbance data from all 3 lab groups
> A_group1 <- c(0.010, 0.011, 0.015, 0.201, 0.373, 0.599, 0.783)
> A_group2 <- c(0.125, 0.242, 0.410, 0.419, 0.641, 0.680, 1.001)
> A_group3 <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> # Combine absorbances into a matrix to calculate Mean and Standard Deviation (SD) per concentration
> A_matrix <- cbind(A_group1, A_group2, A_group3)
> mean_A   <- rowMeans(A_matrix)
> sd_A     <- apply(A_matrix, 1, sd)
> 
> # 3. Create full un-aggregated vectors for linear regression fitting
> C_pooled <- rep(C_single, times = 3)
> A_pooled <- c(A_group1, A_group2, A_group3)
> 
> # 4. Fit the linear regression model using all pooled data points
> pooled_model   <- lm(A_pooled ~ C_pooled)
> model_summary  <- summary(pooled_model)
> 
> # Extract coefficients and regression statistics
> intercept <- coef(pooled_model)["(Intercept)"]
> slope     <- coef(pooled_model)["C_pooled"]
> 
> se_slope  <- model_summary$coefficients["C_pooled", "Std. Error"]
> s_yx      <- model_summary$sigma  # Standard error of the linear regression
> r_squared <- model_summary$r.squared
> 
> # 5. Plot mean absorbance vs. concentration with error bars (Mean ± SD)
> plot(C_single, mean_A,
+      pch = 16, 
+      col = "blue", 
+      cex = 1.3,
+      ylim = c(0, max(mean_A + sd_A) + 0.1),
+      main = "Pooled Aspartame Calibration Curve (Mean ± SD)",
+      xlab = "Concentration (mM)", 
+      ylab = "Mean Absorbance")
> 
> # 6. Add vertical error bars representing ± 1 Standard Deviation
> arrows(x0 = C_single, 
+        y0 = mean_A - sd_A, 
+        x1 = C_single, 
+        y1 = mean_A + sd_A, 
+        length = 0.05, 
+        angle = 90, 
+        code = 3, 
+        col = "darkblue", 
+        lwd = 1.5)
> 
> # 7. Add pooled regression line of best fit
> abline(pooled_model, col = "red", lwd = 2)
> 
> # 8. Annotate plot with regression equation and R^2
> eq_label <- sprintf("y = %.5fx + %.5f\nR² = %.4f", slope, intercept, r_squared)
> legend("topleft", 
+        legend = c("Group Means ± SD", "Line of Best Fit", eq_label), 
+        col = c("blue", "red", NA), 
+        pch = c(16, NA, NA), 
+        lty = c(NA, 1, NA), 
+        lwd = c(NA, 2, NA), 
+        bty = "n", 
+        cex = 0.9)
> 
> # 9. Convert Molar Absorptivity and error to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M    <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print complete Day 2 summary table to Console
> cat("\n================ POOLED DATA LAB REPORT OUTPUTS ================\n")

================ POOLED DATA LAB REPORT OUTPUTS ================
> cat("Regression Equation              : y =", round(slope, 5), "* x +", round(intercept, 5), "\n")
Regression Equation              : y = 0.08898 * x + 0.04258 
> cat("Molar Absorptivity (ε)           :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε)           : 88.98 M^-1 cm^-1
> cat("Std Error in Molar Absorptivity  :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in Molar Absorptivity  : 8.74 M^-1 cm^-1
> cat("Std Error of Linear Regression   :", round(s_yx, 5), "\n")
Std Error of Linear Regression   : 0.13505 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.845 
> cat("=================================================================\n")
=================================================================
> # 1. Standard concentrations (7 unique levels in mM)
> conc_single <- c(0.5, 1, 2, 4, 6, 8, 10)
> C_pooled <- rep(conc_single, times = 3)
> 
> # 2. Absorbance data from all 3 lab groups
> A_group1 <- c(0.010, 0.011, 0.015, 0.201, 0.373, 0.599, 0.783)
> A_group2 <- c(0.125, 0.242, 0.410, 0.419, 0.641, 0.680, 1.001)
> A_group3 <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> A_pooled <- c(A_group1, A_group2, A_group3)
> 
> # 3. Define Group categories (7 data points per group)
> Group <- rep(c("Group 1", "Group 2", "Group 3"), each = 7)
> 
> # 4. Define distinct colors for each group
> group_colors <- c("Group 1" = "blue", "Group 2" = "darkgreen", "Group 3" = "purple")
> 
> # 5. Fit the pooled linear regression model
> pooled_model  <- lm(A_pooled ~ C_pooled)
> model_summary <- summary(pooled_model)
> 
> # Extract coefficients and regression statistics
> intercept <- coef(pooled_model)["(Intercept)"]
> slope     <- coef(pooled_model)["C_pooled"]
> 
> se_slope  <- model_summary$coefficients["C_pooled", "Std. Error"]
> s_yx      <- model_summary$sigma  # Standard error of the linear regression
> r_squared <- model_summary$r.squared
> 
> # 6. Plot individual data points color-coded by group
> plot(C_pooled, A_pooled, 
+      pch = 16, 
+      col = group_colors[Group], 
+      cex = 1.3,
+      main = "Pooled Spectrophotometer Data (Individual Points by Group)",
+      xlab = "Concentration (mM)", 
+      ylab = "Absorbance")
> 
> # 7. Add pooled line of best fit
> abline(pooled_model, col = "red", lwd = 2)
> 
> # 8. Annotate plot with legend showing group colors + line equation & R^2
> eq_label <- sprintf("y = %.5fx + %.5f\nR² = %.4f", slope, intercept, r_squared)
> 
> legend("topleft", 
+        legend = c("Group 1", "Group 2", "Group 3", "Line of Best Fit", eq_label), 
+        col = c("blue", "darkgreen", "purple", "red", NA), 
+        pch = c(16, 16, 16, NA, NA), 
+        lty = c(NA, NA, NA, 1, NA), 
+        lwd = c(NA, NA, NA, 2, NA), 
+        bty = "n", 
+        cex = 0.85)
> 
> # 9. Convert Molar Absorptivity to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M    <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print complete Day 2 summary table to Console
> cat("\n================ POOLED DATA LAB REPORT OUTPUTS ================\n")

================ POOLED DATA LAB REPORT OUTPUTS ================
> cat("Regression Equation              : y =", round(slope, 5), "* x +", round(intercept, 5), "\n")
Regression Equation              : y = 0.08898 * x + 0.04258 
> cat("Molar Absorptivity (ε)           :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε)           : 88.98 M^-1 cm^-1
> cat("Std Error in Molar Absorptivity  :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in Molar Absorptivity  : 8.74 M^-1 cm^-1
> cat("Std Error of Linear Regression   :", round(s_yx, 5), "\n")
Std Error of Linear Regression   : 0.13505 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.845 
> cat("=================================================================\n")
=================================================================
> # 1. Standard concentrations (7 unique levels in mM)
> conc_single <- c(0.5, 1, 2, 4, 6, 8, 10)
> C_pooled <- rep(conc_single, times = 3)
> 
> # 2. Absorbance data from all 3 lab groups
> A_group1 <- c(0.010, 0.011, 0.015, 0.201, 0.373, 0.599, 0.783)
> A_group2 <- c(0.125, 0.242, 0.410, 0.419, 0.641, 0.680, 1.001)
> A_group3 <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> A_pooled <- c(A_group1, A_group2, A_group3)
> 
> # 3. Calculate mean absorbance and standard deviation (SD) for error bars
> A_matrix <- cbind(A_group1, A_group2, A_group3)
> mean_A   <- rowMeans(A_matrix)
> sd_A     <- apply(A_matrix, 1, sd)
> 
> # 4. Group definitions & distinct colors
> Group <- rep(c("Group 1", "Group 2", "Group 3"), each = 7)
> group_colors <- c("Group 1" = "blue", "Group 2" = "darkgreen", "Group 3" = "purple")
> 
> # 5. Fit the pooled linear regression model
> pooled_model  <- lm(A_pooled ~ C_pooled)
> model_summary <- summary(pooled_model)
> 
> intercept <- coef(pooled_model)["(Intercept)"]
> slope     <- coef(pooled_model)["C_pooled"]
> 
> se_slope  <- model_summary$coefficients["C_pooled", "Std. Error"]
> s_yx      <- model_summary$sigma  # Standard error of the linear regression
> r_squared <- model_summary$r.squared
> 
> # 6. Plot individual data points color-coded by group with Y-axis expanded for error bars
> plot(C_pooled, A_pooled, 
+      pch = 16, 
+      col = group_colors[Group], 
+      cex = 1.3,
+      ylim = c(0, max(mean_A + sd_A) + 0.1),
+      main = "Pooled Spectrophotometer Data (Points & Mean Error Bars)",
+      xlab = "Concentration (mM)", 
+      ylab = "Absorbance")
> 
> # 7. Add vertical error bars representing ± 1 SD calculated from group means
> arrows(x0 = conc_single, 
+        y0 = mean_A - sd_A, 
+        x1 = conc_single, 
+        y1 = mean_A + sd_A, 
+        length = 0.05, 
+        angle = 90, 
+        code = 3, 
+        col = "gray40", 
+        lwd = 1.5)
> 
> # 8. Add pooled line of best fit
> abline(pooled_model, col = "red", lwd = 2)
> 
> # 9. Annotate plot with legend showing group colors, error bars + line equation & R^2
> eq_label <- sprintf("y = %.5fx + %.5f\nR² = %.4f", slope, intercept, r_squared)
> 
> legend("topleft", 
+        legend = c("Group 1", "Group 2", "Group 3", "Mean ± SD Error", "Line of Best Fit", eq_label), 
+        col = c("blue", "darkgreen", "purple", "gray40", "red", NA), 
+        pch = c(16, 16, 16, NA, NA, NA), 
+        lty = c(NA, NA, NA, 1, 1, NA), 
+        lwd = c(NA, NA, NA, 1.5, 2, NA), 
+        bty = "n", 
+        cex = 0.8)
> 
> # 10. Convert Molar Absorptivity to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M    <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print complete Day 2 summary table to Console
> cat("\n================ POOLED DATA LAB REPORT OUTPUTS ================\n")

================ POOLED DATA LAB REPORT OUTPUTS ================
> cat("Regression Equation              : y =", round(slope, 5), "* x +", round(intercept, 5), "\n")
Regression Equation              : y = 0.08898 * x + 0.04258 
> cat("Molar Absorptivity (ε)           :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε)           : 88.98 M^-1 cm^-1
> cat("Std Error in Molar Absorptivity  :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in Molar Absorptivity  : 8.74 M^-1 cm^-1
> cat("Std Error of Linear Regression   :", round(s_yx, 5), "\n")
Std Error of Linear Regression   : 0.13505 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.845 
> cat("=================================================================\n")
=================================================================
> # 1. Standard concentrations (7 unique levels in mM)
> conc_single <- c(0.5, 1, 2, 4, 6, 8, 10)
> C_pooled <- rep(conc_single, times = 3)
> 
> # 2. Absorbance data from all 3 lab groups
> A_group1 <- c(0.010, 0.011, 0.015, 0.201, 0.373, 0.599, 0.783)
> A_group2 <- c(0.125, 0.242, 0.410, 0.419, 0.641, 0.680, 1.001)
> A_group3 <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> A_pooled <- c(A_group1, A_group2, A_group3)
> 
> # 3. Calculate mean absorbance and standard deviation (SD) for error bars
> A_matrix <- cbind(A_group1, A_group2, A_group3)
> mean_A   <- rowMeans(A_matrix)
> sd_A     <- apply(A_matrix, 1, sd)
> 
> # 4. Group definitions & distinct colors
> Group <- rep(c("Group 1", "Group 2", "Group 3"), each = 7)
> group_colors <- c("Group 1" = "blue", "Group 2" = "darkgreen", "Group 3" = "purple")
> 
> # 5. Fit the pooled linear regression model
> pooled_model  <- lm(A_pooled ~ C_pooled)
> model_summary <- summary(pooled_model)
> 
> intercept <- coef(pooled_model)["(Intercept)"]
> slope     <- coef(pooled_model)["C_pooled"]
> 
> se_slope  <- model_summary$coefficients["C_pooled", "Std. Error"]
> s_yx      <- model_summary$sigma  # Standard error of the linear regression
> r_squared <- model_summary$r.squared
> 
> # 6. Plot individual data points color-coded by group
> # Added higher ylim boundary (0 to 1.35) so the title and legend have room without clipping
> plot(C_pooled, A_pooled, 
+      pch = 16, 
+      col = group_colors[Group], 
+      cex = 1.2,
+      ylim = c(0, 1.35),
+      main = "Pooled Spectrophotometer Calibration Curve Data",
+      xlab = "Concentration (mM)", 
+      ylab = "Absorbance")
> 
> # 7. Add vertical error bars representing ± 1 SD calculated from group means
> arrows(x0 = conc_single, 
+        y0 = mean_A - sd_A, 
+        x1 = conc_single, 
+        y1 = mean_A + sd_A, 
+        length = 0.04, 
+        angle = 90, 
+        code = 3, 
+        col = "gray40", 
+        lwd = 1.3)
> 
> # 8. Add pooled line of best fit
> abline(pooled_model, col = "red", lwd = 2)
> 
> # 9. Annotate plot with legend showing group colors, error bars + line equation & R^2
> eq_label <- sprintf("y = %.5fx + %.5f\nR² = %.4f", slope, intercept, r_squared)
> 
> legend("topleft", 
+        legend = c("Group 1", "Group 2", "Group 3", "Mean ± SD Error", "Pooled Best Fit", eq_label), 
+        col = c("blue", "darkgreen", "purple", "gray40", "red", NA), 
+        pch = c(16, 16, 16, NA, NA, NA), 
+        lty = c(NA, NA, NA, 1, 1, NA), 
+        lwd = c(NA, NA, NA, 1.3, 2, NA), 
+        bty = "n", 
+        cex = 0.72,
+        y.intersp = 0.85)
> 
> # 10. Convert Molar Absorptivity to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M    <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print complete Day 2 summary table to Console
> cat("\n================ POOLED DATA LAB REPORT OUTPUTS ================\n")

================ POOLED DATA LAB REPORT OUTPUTS ================
> cat("Regression Equation              : y =", round(slope, 5), "* x +", round(intercept, 5), "\n")
Regression Equation              : y = 0.08898 * x + 0.04258 
> cat("Molar Absorptivity (ε)           :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε)           : 88.98 M^-1 cm^-1
> cat("Std Error in Molar Absorptivity  :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in Molar Absorptivity  : 8.74 M^-1 cm^-1
> cat("Std Error of Linear Regression   :", round(s_yx, 5), "\n")
Std Error of Linear Regression   : 0.13505 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.845 
> cat("=================================================================\n")
=================================================================
> # 1. Expand top plot margin to prevent title clipping
> par(mar = c(5, 4, 4, 2) + 0.1)
> 
> # 2. Standard concentrations (7 unique levels in mM)
> conc_single <- c(0.5, 1, 2, 4, 6, 8, 10)
> C_pooled <- rep(conc_single, times = 3)
> 
> # 3. Absorbance data from all 3 lab groups
> A_group1 <- c(0.010, 0.011, 0.015, 0.201, 0.373, 0.599, 0.783)
> A_group2 <- c(0.125, 0.242, 0.410, 0.419, 0.641, 0.680, 1.001)
> A_group3 <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> A_pooled <- c(A_group1, A_group2, A_group3)
> 
> # 4. Calculate mean absorbance and standard deviation (SD) for error bars
> A_matrix <- cbind(A_group1, A_group2, A_group3)
> mean_A   <- rowMeans(A_matrix)
> sd_A     <- apply(A_matrix, 1, sd)
> 
> # 5. Group definitions & distinct colors
> Group <- rep(c("Group 1", "Group 2", "Group 3"), each = 7)
> group_colors <- c("Group 1" = "blue", "Group 2" = "darkgreen", "Group 3" = "purple")
> 
> # 6. Fit the pooled linear regression model
> pooled_model  <- lm(A_pooled ~ C_pooled)
> model_summary <- summary(pooled_model)
> 
> intercept <- coef(pooled_model)["(Intercept)"]
> slope     <- coef(pooled_model)["C_pooled"]
> 
> se_slope  <- model_summary$coefficients["C_pooled", "Std. Error"]
> s_yx      <- model_summary$sigma  # Standard error of the linear regression
> r_squared <- model_summary$r.squared
> 
> # 7. Plot with small title font (cex.main) and extended Y-axis (ylim = c(0, 1.6))
> plot(C_pooled, A_pooled, 
+      pch = 16, 
+      col = group_colors[Group], 
+      cex = 1.0,
+      ylim = c(0, 1.6),
+      main = "Pooled Spectrophotometer Calibration Curve Data",
+      cex.main = 0.9,
+      xlab = "Concentration (mM)", 
+      ylab = "Absorbance")
> 
> # 8. Add vertical error bars representing ± 1 SD
> arrows(x0 = conc_single, 
+        y0 = mean_A - sd_A, 
+        x1 = conc_single, 
+        y1 = mean_A + sd_A, 
+        length = 0.03, 
+        angle = 90, 
+        code = 3, 
+        col = "gray40", 
+        lwd = 1.2)
> 
> # 9. Add pooled line of best fit
> abline(pooled_model, col = "red", lwd = 1.5)
> 
> # 10. Scaled-down legend (cex = 0.60)
> eq_label <- sprintf("y = %.5fx + %.5f\nR² = %.4f", slope, intercept, r_squared)
> 
> legend("topleft", 
+        legend = c("Group 1", "Group 2", "Group 3", "Mean ± SD Error", "Pooled Best Fit", eq_label), 
+        col = c("blue", "darkgreen", "purple", "gray40", "red", NA), 
+        pch = c(16, 16, 16, NA, NA, NA), 
+        lty = c(NA, NA, NA, 1, 1, NA), 
+        lwd = c(NA, NA, NA, 1.2, 1.5, NA), 
+        bty = "n", 
+        cex = 0.60,
+        y.intersp = 0.75)
> 
> # 11. Convert Molar Absorptivity to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M    <- slope * 1000
> se_molar_absorptivity_M <- se_slope * 1000
> 
> # Print complete Day 2 summary table to Console
> cat("\n================ POOLED DATA LAB REPORT OUTPUTS ================\n")

================ POOLED DATA LAB REPORT OUTPUTS ================
> cat("Regression Equation              : y =", round(slope, 5), "* x +", round(intercept, 5), "\n")
Regression Equation              : y = 0.08898 * x + 0.04258 
> cat("Molar Absorptivity (ε)           :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε)           : 88.98 M^-1 cm^-1
> cat("Std Error in Molar Absorptivity  :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in Molar Absorptivity  : 8.74 M^-1 cm^-1
> cat("Std Error of Linear Regression   :", round(s_yx, 5), "\n")
Std Error of Linear Regression   : 0.13505 
> cat("Coefficient of Determination (R2):", round(r_squared, 4), "\n")
Coefficient of Determination (R2): 0.845 
> cat("=================================================================\n")
=================================================================
> # 1. Concentrations (7 standard levels in mM, repeated for 3 lab groups)
> conc_single <- c(0.5, 1, 2, 4, 6, 8, 10)
> C_pooled <- rep(conc_single, times = 3)
> 
> # 2. Absorbance data from all 3 lab groups
> A_group1 <- c(0.010, 0.011, 0.015, 0.201, 0.373, 0.599, 0.783)
> A_group2 <- c(0.125, 0.242, 0.410, 0.419, 0.641, 0.680, 1.001)
> A_group3 <- c(0.086, 0.164, 0.303, 0.524, 0.743, 0.909, 1.064)
> 
> A_pooled <- c(A_group1, A_group2, A_group3)
> 
> # 3. Fit the linear regression model (Beer's Law: A = slope * C)
> pooled_model <- lm(A_pooled ~ C_pooled)
> model_summary <- summary(pooled_model)
> 
> # 4. Extract slope (molar absorptivity in mM^-1 cm^-1 assuming b = 1 cm)
> slope_mM <- coef(pooled_model)["C_pooled"]
> se_slope_mM <- model_summary$coefficients["C_pooled", "Std. Error"]
> 
> # 5. Convert to standard M^-1 cm^-1 units (1 mM = 10^-3 M)
> molar_absorptivity_M <- slope_mM * 1000
> se_molar_absorptivity_M <- se_slope_mM * 1000
> 
> # 6. Extract additional Day 2 required parameters
> s_yx <- model_summary$sigma        # Standard error of linear regression
> r_squared <- model_summary$r.squared # Coefficient of Determination
> 
> # Print results directly to Console
> cat("\n================ POOLED MOLAR ABSORPTIVITY ================\n")

================ POOLED MOLAR ABSORPTIVITY ================
> cat("Molar Absorptivity (ε) :", round(molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Molar Absorptivity (ε) : 88.98 M^-1 cm^-1
> cat("Std Error in ε         :", round(se_molar_absorptivity_M, 2), "M^-1 cm^-1\n")
Std Error in ε         : 8.74 M^-1 cm^-1
> cat("Std Error of Regression:", round(s_yx, 5), "\n")
Std Error of Regression: 0.13505 
> cat("R-squared (R²)         :", round(r_squared, 4), "\n")
R-squared (R²)         : 0.845 
> cat("===========================================================\n")
===========================================================
> 
