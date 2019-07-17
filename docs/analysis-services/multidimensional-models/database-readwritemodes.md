---
title: Banco de dados ReadWriteModes | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e80433c224f08b9074a8d1ef93ef96bdc157853
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178844"
---
# <a name="database-readwritemodes"></a>Banco de dados ReadWriteModes
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Existem situações frequentes em que um DBA (administrador de banco de dados) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quer alterar o banco de dados de leitura/gravação para um banco de dados somente leitura ou vice-versa. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como o compartilhamento da mesma pasta do banco de dados com vários servidores para expandir uma solução e melhorar o desempenho. Para estas situações, a propriedade **ReadWriteMode** do banco de dados permite que o DBA do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] altere facilmente o modo de operação do banco de dados.  
  
## <a name="readwritemode-database-property"></a>Propriedade ReadWriteMode do banco de dados  
 A propriedade do banco de dados **ReadWriteMode** especifica se o banco de dados está no modo leitura/gravação ou no modo somente leitura. Estes são os únicos dois possíveis valores da propriedade. Quando o banco de dados está no modo somente leitura, nenhuma alteração ou atualização pode ser aplicada a ele. Entretanto, quando o banco de dados está no modo de leitura/gravação, podem ocorrer alterações e atualizações. A propriedade **ReadWriteMode** do banco de dados está definida como uma propriedade somente leitura; ela só pode ser definida por um comando **Attach** .  
  
 Quando um banco de dados é definido para o modo somente leitura, determinadas restrições entram em vigor e afetam o conjunto comum das operações permitidas no banco de dados. Consulte a tabela a seguir para obter as operações restritas.  
  
|Modo ReadOnly|Operações restritas|  
|-------------------|---------------------------|  
|Comandos XML/A<br /><br /> <br /><br /> Observação: Um erro é gerado quando você executa qualquer um desses comandos.|**Criar**<br /><br /> **Alter**<br /><br /> **Delete (excluir)**<br /><br /> **Processar**<br /><br /> **MergePartitions**<br /><br /> **DesignAggregations**<br /><br /> **CommitTransaction**<br /><br /> **Restaurar**<br /><br /> **Sincronizar**<br /><br /> **Inserir**<br /><br /> **Update (atualizar)**<br /><br /> **Drop**<br /><br /> <br /><br /> Observação: Write-back de célula é permitido em bancos de dados definidos como somente leitura; No entanto, as alterações não podem ser confirmadas.|  
|Instruções MDX<br /><br /> <br /><br /> Observação: Um erro é gerado quando você executa qualquer uma dessas instruções.|**COMMIT TRAN**<br /><br /> **CREATE SESSION CUBE**<br /><br /> **ALTER CUBE**<br /><br /> **ALTER DIMENSION**<br /><br /> **CREATE DIMENSION MEMBER**<br /><br /> **DROP DIMENSION MEMBER**<br /><br /> **ALTER DIMENSION**<br /><br /> <br /><br /> Observação: Os usuários do Excel não é possível usar o recurso de agrupamento em tabelas dinâmicas, pois esse recurso é implementado internamente usando **CREATE SESSION CUBE** comandos.|  
|Instruções DMX<br /><br /> <br /><br /> Observação: Um erro é gerado quando você executa qualquer uma dessas instruções.|**CREATE [SESSION] MINING STRUCTURE**<br /><br /> **ALTER MINING STRUCTURE**<br /><br /> **DROP MINING STRUCTURE**<br /><br /> **CREATE [SESSION] MINING MODEL**<br /><br /> **DROP MINING MODEL**<br /><br /> **IMPORT**<br /><br /> **SELECT INTO**<br /><br /> **INSERT**<br /><br /> **UPDATE**<br /><br /> **DELETE**|  
|Operações em segundo plano|Todas as operações em segundo plano que poderiam modificar o banco de dados são desabilitadas. Isso inclui o processamento lento e o cache pró-ativo.|  
  
## <a name="readwritemode-usage"></a>Uso de ReadWriteMode  
 A propriedade **ReadWriteMode** do banco de dados será usada como parte de um comando **Attach** do banco de dados. O comando **Attach** permite que a propriedade do banco de dados seja definida como **ReadWrite** ou **ReadOnly**. O valor da propriedade **ReadWriteMode** do banco de dados não pode ser atualizado diretamente, pois a propriedade está definida como somente leitura. Os bancos de dados são criados com a propriedade **ReadWriteMode** definida como **ReadWrite**. Um banco de dados não pode ser criado no modo somente leitura.  
  
 Para mudar a propriedade de banco de dados **ReadWriteMode** entre **ReadWrite** e **ReadOnly**, é necessário emitir uma sequência de comandos **Detach/Attach** .  
  
 Todas as operações do banco de dados, com exceção de **Attach**, mantêm a propriedade **ReadWriteMode** do banco de dados em seu estado atual. Por exemplo, operações como **Alter**, **Backup**, **Restore**e **Synchronize** preservam o valor **ReadWriteMode** .  
  
> [!NOTE]  
>  Podem ser criados cubos locais a partir de um banco de dados somente leitura.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Anexar e desanexar Bancos de Dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover um Banco de Dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  
