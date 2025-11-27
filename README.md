import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

#importation de mon dataset
work=pd.read_csv('/storage/emulated/0/Android/media/com.transsion.phoenix/PHX_Archive/phx_extracted/archive(2)/MFGEmployees4.csv' , nrows=100)
X=work['AbsentHours']
Y=work['EmployeeNumber']

#création d'une carte de chaleur avec heatmap de seaborn'
sns.heatmap(pd.DataFrame(X) )
plt.title( "Absentéisme des employés chez IBM")
plt.show()

#création d'un diagramme en camembert avec plt.pie'
C=pd.DataFrame({'heures':X})
bornes=[0,10,20,30,40,50,60,70,80,90,100]
labels=['Bon employé :0-10','Avertissement :10-20','Blâme conduite :20-30','Mise à pieds :30-40','Sanctions pécuniaires :40-50',' ( À partir de cette catégorie , licenciement ):50-60','60-70','70-80','80-90','90-100']
C['heure']=pd.cut(C['heures'],bins=bornes,labels=labels,include_lowest=True)
effectifs=C['heure'].value_counts().sort_index()
plt.pie(effectifs,labels=effectifs.index)
plt.legend( title="Statut selon le nombre d'heures d'absences")
plt.title("Absence des employés")
plt.axis('equal')
plt.show()
