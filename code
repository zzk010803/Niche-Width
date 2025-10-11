
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

file_path = r"otu_copies.csv"
otu_df = pd.read_csv(file_path)

high_samples = ["test_1", "test_2"]
low_samples = ["test_3", "test_4"]

def calc_niche_breadth(row):
    total = row.sum()
    if total == 0:
        return 0
    p = row / total
    return 1 / (p ** 2).sum()

results = []
for group_name, sample_list in [("GW20", high_samples), ("GW22", low_samples)]:
    group_abund = otu_df[sample_list].copy()
    rel_abund = group_abund.div(group_abund.sum(axis=0), axis=1)  
    mean_rel_abund = rel_abund.mean(axis=1)
    bi_values = group_abund.apply(calc_niche_breadth, axis=1)

    group_df = pd.DataFrame({
        "OTU_ID": otu_df["#OTU ID"],
        "Group": group_name,
        "Bi": bi_values,
        "Mean_RelAbund": mean_rel_abund
    })

    results.append(group_df)

plot_df = pd.concat(results, ignore_index=True)

plot_df = plot_df[plot_df["Mean_RelAbund"] > 0].copy()
plot_df["log10_Abund"] = np.log10(plot_df["Mean_RelAbund"])

g = sns.JointGrid(data=plot_df, x="log10_Abund", y="Bi", hue="Group", height=6)

g.plot_joint(sns.scatterplot, alpha=0.6, s=20)

g.plot_marginals(sns.kdeplot, fill=True, common_norm=False, alpha=0.3, linewidth=1)

g.ax_joint.set_xlim(-5.5, -1)
g.ax_joint.set_ylim(1.1, 2.1)

g.ax_joint.set_xlabel("Mean Relative Abundance (log10 scale)")
g.ax_joint.set_ylabel("Bi (Niche Breadth)")
g.ax_joint.set_title("OTU Niche Breadth vs. Relative Abundance", pad=70)

g.ax_joint.legend(title="Group", loc="upper left")
plt.tight_layout()

plt.savefig("niche width.pdf", format="pdf", bbox_inches="tight")
plt.show()
