---
title: "Representação em modelos de tabela do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 6d18cbe5b20882581afa731ce5d207cbbc69be6c
ms.openlocfilehash: aef09b5327408701f15e484bbcea1cab9d82622b
ms.contentlocale: pt-br
ms.lasthandoff: 10/21/2017

---
# <a name="impersonation"></a>Representação 

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Este tópico fornece a autores de modelo de tabela uma compreensão de como as credenciais de logon são usadas pelo Analysis Services ao conectar-se a uma fonte de dados para importar e processar (Atualizar) dados.  

##  <a name="bkmk_conf_imp_info"></a>Configurando a representação  
 Onde e o contexto existe um modelo determina como as informações de representação são configuradas. Ao criar um novo projeto de modelo, a representação está configurada no SQL Server Data Tools (SSDT) quando você se conectar a uma fonte de dados para importar dados. Depois que um modelo é implantado, representação pode ser configurada na propriedade de cadeia de caracteres de conexão de banco de dados de modelo usando o SQL Server Management Studio (SSMS). Para modelos de tabela no Azure Analysis Services, você pode usar o SSMS ou o **exibir como: Script** modo no designer e baseada em navegador para editar o arquivo Model.bim em JSON.
  
##  <a name="bkmk_how_imper"></a>Como a representação é usada  
 *Representação* é a capacidade de um aplicativo de servidor, como o Analysis Services, de assumir a identidade de um aplicativo cliente. Analysis Services é executado usando uma conta de serviço, no entanto, quando o servidor estabelece uma conexão a uma fonte de dados, ele usa representação para que as verificações de acesso para importação de dados e o processamento pode ser executado.  
  
 As credenciais usadas para representação são diferentes das credenciais do qual com que você fez logon. As credenciais são usadas para operações de cliente específicas ao criar um modelo de usuário conectado.  
  
 É importante compreender como as credenciais de representação são especificadas e protegidas, bem como a diferença entre contextos nos quais ambas as suas conectado no são usadas as credenciais do usuário e outras credenciais de representação são usadas.  
  
 **Compreendendo as credenciais do lado do servidor**  
 
Quando dados são importados ou processados, as credenciais de representação são usadas para se conectar à fonte de dados e buscar os dados. Este é um *do lado do servidor* operação sendo executada no contexto de um aplicativo cliente porque o servidor do Analysis Services que hospeda o banco de dados do espaço de trabalho conecta-se à fonte de dados e busca os dados.  
  
 Ao implantar um modelo no servidor do Analysis Services, se o banco de dados de espaço de trabalho estiver na memória quando o modelo for implantado, as credenciais serão passadas para o servidor do Analysis Services para o qual o modelo é implantado. Em nenhum momento as credenciais de usuário armazenados em disco.  
  
 Quando um modelo implantado processa dados de uma fonte de dados, as credenciais de representação, persistidas no banco de dados na memória são usadas para se conectar à fonte de dados e buscar os dados. Como esse processo é tratado pelo servidor do Analysis Services que gerencia o banco de dados de modelo, isso novamente é uma operação do servidor.  
  
 **Compreendendo as credenciais de cliente**  
  
 Quando criar um novo modelo ou adicionar uma fonte de dados a um modelo existente, você se conectar a uma fonte de dados e selecionar tabelas e exibições a serem importados para o modelo. Os Assistente de importação de tabela ou obter Data\Query Designer visualizar e filtrar recursos, verá um exemplo dos dados que você importar. Você também pode especificar filtros para excluir dados que não precisam ser incluídos no modelo.  
  
 Da mesma forma, para modelos existentes que já foram criados, use o **propriedades da tabela** caixa de diálogo para visualizar e filtrar dados importados em uma tabela.  
  
 Os recursos de visualização e filtro, **propriedades da tabela**, e **Gerenciador de partições** caixas de diálogo são um processo de- *cliente* operação; ou seja, o que é feito durante esta operação são diferentes de como a fonte de dados está conectado ao e dados são buscados da fonte de dados; uma operação do servidor. As credenciais usadas para visualizar e filtrar dados são as credenciais do usuário que está conectado no momento. Em efeito, suas credenciais. 
  
 A separação de credenciais usadas durante do lado do servidor e as operações do cliente podem levar a uma incompatibilidade no que você vê e quais dados são buscados durante uma importação ou processamento (uma operação do servidor). Se as credenciais você efetuou logon com e as credenciais de representação especificadas forem diferentes, os dados que você vê nas visualizar e filtrar recursos ou o **propriedades da tabela** caixa de diálogo e os dados buscados durante uma importação ou processo pode ser diferente, dependendo das credenciais requeridas pela fonte de dados.  
  
> [!IMPORTANT]  
>  Ao criar um modelo, verifique se as credenciais de com que logon e as credenciais especificadas para representação têm direitos suficientes para buscar os dados da fonte de dados.  
  
##  <a name="bkmk_imp_info_options"></a> Opções  
 Ao configurar a representação, ou ao editar as propriedades de uma conexão de fonte de dados existente, especifique uma das seguintes opções:  
  
**Modelos de tabela 1400 e superior**
 
|Opção|Description|  
|------------|-----------------|  
|**Representar a conta**|Especifica o modelo usa uma conta de usuário do Windows para importar ou processar dados da fonte de dados. O domínio e o nome da conta de usuário usa o seguinte formato:**\<nome de domínio >\\< nome da conta de usuário\>**.|  
|**Representar o usuário atual**|Especifica os dados devem ser acessados da fonte de dados usando a identidade do usuário que enviou a solicitação. Este modo aplica-se somente ao modo consulta direta.|  
|**Representar a identidade**|Especifica um nome de usuário para acessar a fonte de dados, mas não precisa especificar a senha da conta. Esse modo se aplica somente quando a delegação Kerberos está habilitada e especifica que a autenticação S4U deve ser usada.|  
|**Representar a conta de serviço**|Especifica o modelo usa as credenciais de segurança associadas com a instância do serviço Analysis Services que gerencia o modelo.|  
|**Representar a conta autônoma**|Especifica que o mecanismo do Analysis Services deve usar uma conta autônoma pré-configurado para acessar os dados.|  


**Modelos de tabela 1200**
 
|Opção|Description|  
|------------|-----------------|  
|**Senha e nome de usuário específico do Windows**|Esta opção especifica o modelo usa uma conta de usuário do Windows para importar ou processar dados da fonte de dados. O domínio e o nome da conta de usuário usa o seguinte formato:**\<nome de domínio >\\< nome da conta de usuário\>**. Ao criar um novo modelo por meio do Assistente de Importação de Tabela, essa é a opção padrão.|  
|**Conta de Serviço**|Esta opção especifica que o modelo usa as credenciais de segurança associadas à instância de serviço do Analysis Services que gerencia o modelo.|  
  
##  <a name="bkmk_impers_sec"></a> Segurança  
 As credenciais usadas com representação são persistidas na memória pelo mecanismo de VertiPaq™. As credenciais não são gravadas no disco. Se o banco de dados do espaço de trabalho não estiver na memória quando o modelo é implantado, o usuário é solicitado a inserir as credenciais usadas para conexão com as fonte de dados e buscar dados.  
  
> [!NOTE]  
>  É recomendável especificar uma conta de usuário do Windows e uma senha para credenciais de representação. Uma conta de usuário do Windows pode ser configurada para usar privilégios mínimos necessários para conectar e ler os dados da fonte de dados.  
  

  
## <a name="see-also"></a>Consulte também  
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Fontes de dados](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Implantação de solução de modelo de tabela](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
