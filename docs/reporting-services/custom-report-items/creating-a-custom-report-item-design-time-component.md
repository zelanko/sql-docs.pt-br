---
title: "Criando um componente de tempo de Design de Item de relatório personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0b1f5649db2f99957ad3b2452b02d2f7b2db01cb
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-report-item-design-time-component"></a>Criando um componente de tempo de design de item de relatório personalizado
  Um componente em tempo de design de item de relatório personalizado é um controle que pode ser usado no ambiente do Designer de Relatórios do Visual Studio. O componente em tempo de design de item de relatório personalizado oferece uma superfície de design ativada que pode aceitar operações de arrastar e soltar, a integração ao pesquisador de propriedade [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e a capacidade de oferecer editores de propriedade personalizados.  
  
 Com um componente em tempo de design de item de relatório personalizado, o usuário pode posicionar um item de relatório personalizado em um relatório no ambiente de design, definir propriedades de dados personalizadas no item de relatório personalizado e, depois, salvar esse item como parte do projeto de relatório.  
  
 As propriedades definidas usando o componente em tempo de design no ambiente de desenvolvimento são serializadas e desserializadas pelo ambiente de design de host e, depois, armazenadas como elementos no arquivo em linguagem RDL. Quando o relatório é executado pelo processador de relatório, as propriedades definidas usando o componente em tempo de design são passadas pelo processador de relatório para um componente em tempo de execução de item de relatório personalizado, que renderiza o item de relatório personalizado e o devolve ao processador de relatório.  
  
> [!NOTE]  
>  O componente de tempo de design de item de relatório personalizado é implementado como um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] componente. Este documento descreverá detalhes de implementação específicos do componente em tempo de design de item de relatório personalizado. Para obter mais informações sobre como desenvolver componentes usando o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte [componentes no Visual Studio](http://go.microsoft.com/fwlink/?LinkId=116576) na biblioteca MSDN.  
  
 Para obter um exemplo de um item de relatório personalizado totalmente implementado, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="implementing-a-design-time-component"></a>Implementando um componente em tempo de design  
 A classe principal de um componente de tempo de design de item de relatório personalizado é herdada da **Microsoft.ReportDesigner.CustomReportItemDesigner** classe. Além dos atributos padrão usados para um [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] controle, a classe de componente deve definir um **CustomReportItem** atributo. Esse atributo deve corresponder ao nome do item de relatório personalizado conforme definido no arquivo reportserver.config. Para obter uma lista de atributos do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte Atributos na documentação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 O seguinte exemplo de código mostra atributos que estão sendo aplicados a um controle em tempo de design de item de relatório personalizado:  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>Inicializando o componente  
 Você passa propriedades especificadas pelo usuário para um item de relatório personalizado usando uma classe <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>. A implementação do **CustomReportItemDesigner** classe deve substituir o **InitializeNewComponent** método para criar uma nova instância do seu componente <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> classe e defina-a como valores padrão.  
  
 O exemplo de código a seguir mostra um exemplo de um componente de tempo de design de item de relatório personalizado na substituição do classe o **CustomReportItemDesigner.InitializeNewComponent** método para inicializar o componente <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> classe:  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>Modificando propriedades do componente  
 Você pode modificar **CustomData** propriedades no ambiente de design de várias maneiras. Você pode modificar quaisquer propriedades expostas pelo componente em tempo de design que estejam marcadas com o atributo <xref:System.ComponentModel.BrowsableAttribute> usando o pesquisador de propriedade do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Além disso, você pode modificar propriedades arrastando itens para a superfície de design do item de relatório personalizado, ou clicando duas vezes o controle no ambiente de design e selecionando **propriedades** no menu de atalho para exibir uma janela de propriedades personalizadas.  
  
 O seguinte exemplo de código mostra uma **Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData** propriedade que tem o <xref:System.ComponentModel.BrowsableAttribute> atributo aplicado:  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 Você pode fornecer ao componente em tempo de design uma caixa de diálogo de editor de propriedades personalizadas. A implementação do editor de propriedades personalizadas deve ser herdada da classe <xref:System.ComponentModel.ComponentEditor> e deve criar uma instância de uma caixa de diálogo a ser usada na edição de propriedades.  
  
 O seguinte exemplo mostra uma implementação de uma classe herdada de <xref:System.ComponentModel.ComponentEditor> e exibe uma caixa de diálogo de editor de propriedade personalizadas:  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 Sua caixa de diálogo de editor de propriedades personalizadas pode invocar o Editor de Expressão do Designer de Relatórios. Neste exemplo, o Editor de Expressão é invocado quando o usuário seleciona o primeiro elemento na caixa de combinação:  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>Usando verbos do designer  
 Um verbo do designer é um comando de menu vinculado a um manipulador de eventos. Você pode adicionar verbos do designer que aparecerão no menu de atalho de um componente quando o controle em tempo de execução do seu item de relatório personalizado estiver sendo usado no ambiente de design. Você pode retornar a lista de verbos do designer disponíveis de seu componente de tempo de execução usando o **verbos** propriedade.  
  
 Este exemplo de código mostra um verbo do designer e um manipulador de eventos que está sendo adicionado ao <xref:System.ComponentModel.Design.DesignerVerbCollection>, bem como o código do manipulador de eventos:  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>Usando adornos  
 Classes de item de relatório personalizado também podem implementar um **Microsoft.ReportDesigner.Design.Adornment** classe. Um adorno permite que o controle de item de relatório personalizado forneça áreas fora do retângulo principal da superfície de design. Essas áreas podem tratar eventos de interface do usuário, tais como cliques de mouse e operações de arrastar e soltar. O **adorno** classe definida no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **reportdesigner** namespace é uma implementação de passagem a <xref:System.Windows.Forms.Design.Behavior.Adorner> classe encontrada em formulários do Windows. Para obter a documentação completa sobre o **adorno** de classe, consulte [visão geral do serviço de comportamento](http://go.microsoft.com/fwlink/?LinkId=116673) na biblioteca MSDN. Para o código de exemplo que implementa um **Microsoft.ReportDesigner.Design.Adornment** de classe, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
 Para obter mais informações sobre como programar e usar o Windows Forms no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], consulte estes tópicos no biblioteca MSDN:  
  
-   Atributos em tempo de design para componentes  
  
-   Componentes do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]  
  
-   Passo a passo: Criando um controle do Windows Forms que aproveita recursos em tempo de design do Visual Studio  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura de Item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [Criando um componente de tempo de execução do Item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Bibliotecas de classe de Item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [Como: implantar um Item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
