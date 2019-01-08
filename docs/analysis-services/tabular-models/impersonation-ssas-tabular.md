---
title: Representação em modelos de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 724d9220f156cb9b2a00e3bd12a15f35750de652
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416006"
---
# <a name="impersonation"></a>Representação 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo fornece a autores de modelos tabulares uma compreensão de como as credenciais de logon são usadas pelo Analysis Services ao se conectar a uma fonte de dados para importar e processar (Atualizar) dados.  

##  <a name="bkmk_conf_imp_info"></a> Configurando a representação  
 Onde e o contexto existe um modelo determina como as informações de representação são configuradas. Ao criar um novo projeto de modelo, a representação é configurada no SSDT SQL Server Data Tools () quando você se conecta a uma fonte de dados para importar dados. Depois que um modelo é implantado, representação pode ser configurada na propriedade de cadeia de conexão de banco de dados de modelo usando o SQL Server Management Studio (SSMS). Para modelos tabulares no Azure Analysis Services, você pode usar o SSMS ou o **exibir como: Script** modo no designer e baseada em navegador para editar o arquivo Model. BIM em JSON.
  
##  <a name="bkmk_how_imper"></a> Como a representação é usada  
 *Representação* é a capacidade de um aplicativo de servidor, como o Analysis Services, de assumir a identidade de um aplicativo cliente. Analysis Services é executado usando uma conta de serviço, no entanto, quando o servidor estabelece uma conexão a uma fonte de dados, ele usa representação para que as verificações de acesso para importação de dados e processamento pode ser executado.  
  
 As credenciais usadas para representação são diferentes das credenciais que você fez logon com. Credenciais são usadas para operações específicas do lado do cliente ao criar um modelo do usuário conectado.  
  
 É importante entender como as credenciais de representação são especificadas e protegidas, bem como a diferença entre contextos nos quais os dois de logon em credenciais do usuário são usadas e quando outras credenciais de representação são usados.  
  
 **Compreendendo as credenciais do lado do servidor**  
 
Quando dados são importados ou processados, credenciais de representação usadas para se conectar à fonte de dados e buscar os dados. Esse é um *servidor* operação sendo executada no contexto de um aplicativo cliente porque o servidor do Analysis Services que hospeda o banco de dados do espaço de trabalho conecta-se à fonte de dados e busca os dados.  
  
 Ao implantar um modelo no servidor do Analysis Services, se o banco de dados de workspace estiver na memória quando o modelo for implantado, as credenciais serão passadas para o servidor do Analysis Services para o qual o modelo é implantado. Em nenhum momento as credenciais de usuário armazenados em disco.  
  
 Quando um modelo implantado processa dados de uma fonte de dados, as credenciais de representação, persistidas no banco de dados na memória, são usadas para se conectar à fonte de dados e buscar os dados. Porque esse processo é tratado pelo servidor do Analysis Services, gerenciando o banco de dados de modelo, isso novamente é uma operação do lado do servidor.  
  
 **Compreendendo as credenciais do lado do cliente**  
  
 Quando um novo modelo de criação ou adição de uma fonte de dados a um modelo existente, você se conectar a uma fonte de dados e seleciona tabelas e exibições a serem importados para o modelo. Os Assistente de importação de tabela ou obter Data\Query Designer visualizar e filtrar recursos, você verá uma amostra dos dados importados por você. Você também pode especificar filtros para excluir dados que não precisam ser incluídos no modelo.  
  
 Da mesma forma, para modelos existentes que já foram criados, use o **propriedades da tabela** caixa de diálogo para visualizar e filtrar dados importados para uma tabela.  
  
 Visualizar e filtrar recursos, **propriedades da tabela**, e **Gerenciador de partições** caixas de diálogo são um processo de- *lado do cliente* operação; ou seja, o que é feito durante este operação são diferentes de como a fonte de dados está conectado e os dados são buscados da fonte de dados; uma operação do lado do servidor. As credenciais usadas para visualizar e filtrar dados são as credenciais do usuário que está conectado no momento. Efeito, suas credenciais. 
  
 A separação de credenciais usadas durante o lado do servidor e operações do lado do cliente podem levar a uma incompatibilidade no que você vê e quais dados são buscados durante uma importação ou processamento (uma operação do lado do servidor). Se as credenciais você efetuou logon com e as credenciais de representação especificadas forem diferentes, os dados que você verá nos recursos de visualização e filtro ou o **propriedades da tabela** caixa de diálogo e os dados buscados durante uma importação ou processo pode ser diferente, dependendo das credenciais requeridas pela fonte de dados.  
  
> [!IMPORTANT]  
>  Ao criar um modelo, verifique se as credenciais de com que logon e as credenciais especificadas para representação têm direitos suficientes para buscar os dados da fonte de dados.  
  
##  <a name="bkmk_imp_info_options"></a> Opções  
 Ao configurar a representação, ou ao editar as propriedades para uma conexão de fonte de dados existente, especifique uma das opções a seguir:  
  
**Modelos de tabela 1400 e superior**
 
|Opção|Descrição|  
|------------|-----------------|  
|**Representar conta**|Especifica o modelo usa uma conta de usuário do Windows para importar ou processar dados da fonte de dados. O domínio e o nome da conta de usuário usa o seguinte formato:**\<nome de domínio >\\< nome da conta de usuário\>**.|  
|**Representar usuário atual**|Especifica que dados devem ser acessados da fonte de dados usando a identidade do usuário que enviou a solicitação. Esse modo se aplica somente ao modo consulta direta.|  
|**Representar identidade**|Especifica um nome de usuário para acessar a fonte de dados, mas não precisa especificar a senha da conta. Esse modo se aplica somente quando a delegação de Kerberos está habilitada e especifica que a autenticação S4U deve ser usada.|  
|**Representar conta de serviço**|Especifica o modelo usa as credenciais de segurança associadas com a instância do serviço do Analysis Services que gerencia o modelo.|  
|**Representar conta autônoma**|Especifica que o mecanismo do Analysis Services deve usar uma conta autônoma pré-configuradas para acessar os dados.|  


**Modelos de tabela 1200**
 
|Opção|Descrição|  
|------------|-----------------|  
|**Senha e nome de usuário específicos do Windows**|Esta opção especifica o modelo usa uma conta de usuário do Windows para importar ou processar dados da fonte de dados. O domínio e o nome da conta de usuário usa o seguinte formato:**\<nome de domínio >\\< nome da conta de usuário\>**. Ao criar um novo modelo por meio do Assistente de Importação de Tabela, essa é a opção padrão.|  
|**Conta de Serviço**|Esta opção especifica que o modelo usa as credenciais de segurança associadas à instância de serviço do Analysis Services que gerencia o modelo.|  
  
##  <a name="bkmk_impers_sec"></a> Segurança  
 As credenciais usadas com representação são persistidas na memória pelo mecanismo de VertiPaq™. Credenciais nunca são gravadas no disco. Se o banco de dados do espaço de trabalho não estiver na memória quando o modelo é implantado, o usuário é solicitado a inserir as credenciais usadas para conexão com as fonte de dados e buscar dados.  
  
> [!NOTE]  
>  É recomendável especificar uma conta de usuário do Windows e uma senha para credenciais de representação. Uma conta de usuário do Windows pode ser configurada para usar privilégios mínimos necessários para conectar e ler dados da fonte de dados.  
  

  
## <a name="see-also"></a>Confira também  
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Fontes de dados](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Implantação de solução de modelo tabular](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
