---
title: O que são Atualizações de Segurança Estendidas?
description: Saiba como usar o Registro do SQL Server para obter Atualizações de Segurança Estendidas para os produtos de fim de suporte e fim da vida do SQL Server, como o SQL Server 2008 e o SQL Server 2008 R2.
ms.custom: ''
ms.date: 12/09/2019
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: pmasl
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3e585b0314b6306bdff84b07f2d12514ee015936
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900539"
---
# <a name="what-are-extended-security-updates-for-sql-server"></a>Quais são as Atualizações de Segurança Estendidas para o SQL Server?
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

Este artigo fornece informações sobre como usar o serviço de Registro do SQL Server para receber Atualizações de Segurança Estendidas para [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]. Para obter mais informações sobre outras opções, confira as [opções de fim de suporte](sql-server-end-of-life-overview.md). 

## <a name="overview"></a>Visão geral
Depois que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver atingido o fim de seu ciclo de vida de suporte, você terá a opção de se inscrever para uma assinatura de ESU (Atualizações de Segurança Estendidas) para seus servidores e permanecer protegido por até três anos, até que você esteja pronto para atualizar para uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou migrar para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Essa assinatura está disponível de duas maneiras:
-  Pode ser comprada para seus servidores de ambiente locais ou hospedados.
-  Gratuita e habilitada por padrão ao migrar servidores locais para Máquinas Virtuais do Azure. Então você pode usar o serviço de **Registro do SQL Server** no portal do Azure para registrar sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de fim de suporte e baixar atualizações quando elas forem disponibilizadas. 

A Microsoft recomenda aplicar patches de ESU assim que eles estiverem disponíveis para manter sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] protegida. Para obter informações detalhadas sobre ESUs, confira a página de perguntas frequentes da [ESU](https://www.microsoft.com/cloud-platform/extended-security-updates).

> [!IMPORTANT]
> [O suporte estendido para o SQL Server 2008 e SQL Server 2008 R2 terminou em 10 de julho de 2019](https://www.microsoft.com/cloud-platform/windows-sql-server-2008). Para essas versões, considere usar as atualizações de segurança estendidas descritas neste artigo ou outras opções de migração. Para obter mais informações, confira [Opções de fim de suporte](sql-server-end-of-life-overview.md).

## <a name="what-are-extended-security-updates"></a>O que são Atualizações de Segurança Estendidas
As ESUs (Atualizações de Segurança Estendidas) para [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] incluem o provisionamento de atualizações de segurança para clientes que adquiriram uma assinatura de atualização de suporte estendida.

As ESUs serão disponibilizadas **se necessário**, depois que uma vulnerabilidade de segurança for descoberta e classificada como **Crítica** pelo [MSRC (Microsoft Security Response Center)](https://portal.msrc.microsoft.com). Portanto, não há um ritmo regular de versão para ESUs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

As ESUs não incluem:
- Novos recursos
- Aprimoramentos funcionais
- Correções solicitadas pelo cliente

### <a name="support"></a>Suporte
As ESUs não incluem suporte técnico, mas você poderá usar um contrato de suporte ativo, como [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default?activetab=software-assurance-default-pivot%3aprimaryr3) ou Suporte Premier/Unificado no [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] / [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] para obter suporte técnico em cargas de trabalho cobertas pelas ESUs se optar por permanecer no local. Como alternativa, se você estiver hospedando no Azure, poderá usar um plano de Suporte do Azure para obter suporte técnico. 

  > [!NOTE]
  > A Microsoft não pode fornecer suporte técnico para instâncias de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] (locais e em ambientes de hospedagem) não cobertas por uma assinatura de ESU. 

## <a name="esu-availability-and-deployment"></a>Disponibilidade e implantação da ESU
As ESUs estão disponíveis para clientes que executam sua carga de trabalho no Azure, localmente ou em ambientes hospedados.

### <a name="azure-virtual-machines"></a>Máquinas Virtuais do Azure
Se você migrar suas cargas de trabalho para as máquinas virtuais do Azure (IaaS), terá acesso a atualizações de segurança estendidas para [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] por até três anos após o fim do suporte, **sem preço adicional** além do custo da execução da máquina virtual. Os clientes não precisam do Software Assurance para receberem Atualizações de Segurança Estendidas no Azure. 

As Máquinas Virtuais do Azure que executam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no **Windows Server 2008 R2 e versões posteriores** receberão ESUs automaticamente por meio de canais de atualização [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existentes quando a máquina virtual estiver configurada para usar a [aplicação de patch automatizada](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching).

As VMs (Máquinas Virtuais) do Azure que executam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em **Windows Server 2008** ou VMs que ***não* foram configuradas para [aplicação de patch automatizada](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)** precisarão baixar e implantar manualmente os patches da ESU, conforme descrito na seção [ambientes locais ou hospedados](#on-premises-or-hosted-environments).

### <a name="on-premises-or-hosted-environments"></a>Ambientes locais ou hospedados
Se você tiver o Software Assurance, poderá comprar uma assinatura da ESU (Atualização de Segurança Estendida) por até três anos após o fim da data de suporte, em um EA (Contrato Enterprise), EAS (Contrato Enterprise Subscription), um SCE (Registro de Servidor e Nuvem) ou um EES (Registro para Soluções de Educação). Você pode comprar ESUs somente para os servidores que precisa cobrir. As ESUs podem ser compradas diretamente da Microsoft ou de um parceiro de licenciamento da Microsoft. 

Os clientes cobertos por contratos da ESU devem seguir estas etapas para baixar e implantar um patch da ESU:
-  [Registre as instâncias qualificadas](#register-instances-for-esus) com o **[Registro do SQL Server](#create-sql-server-registry)** . 
-  Depois de registradas, sempre que os patches da ESU forem liberados, um link de download estará disponível no portal do Azure para baixar o pacote. 
-  O pacote baixado pode ser implantado em seus ambientes locais ou hospedados manualmente ou por meio de qualquer solução de orquestração de atualização usada em sua organização, como o Microsoft Endpoint Configuration Manager (antigo System Center Configuration Manager). 

> [!NOTE]
> Esse também é o processo que os clientes precisarão seguir para o Azure Stack e as máquinas virtuais do Azure que não estão configuradas para o recebimento de atualizações automáticas.

Para obter mais informações, confira as [perguntas frequentes sobre Atualizações de Segurança Estendidas](https://www.microsoft.com/cloud-platform/extended-security-updates). 

## <a name="create-sql-server-registry"></a>Criar o Registro do SQL Server
Para registrar suas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilitadas para ESU, primeiro crie o Registro do SQL Server no portal do Azure. 

> [!IMPORTANT]
> Não é necessário registrar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ESUs ao executar uma máquina virtual do Azure configurada para [atualizações automáticas](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching). 

Para criar o Registro do SQL Server, siga estas etapas:

1. Faça logon no [Portal do Azure](https://portal.azure.com). 
1. Selecione a opção **Criar um recurso**. 
1. Digite `SQL Server registry` na caixa de pesquisa.  
1. Escolha a opção **Registro do SQL Server** publicada pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] e, em seguida, selecione **Criar**. 

   ![Escolha o serviço de Registro do SQL Server](media/sql-server-extended-security-updates/sql-server-registry-service.png)

1. Em **Detalhes do Projeto**, escolha sua assinatura na lista suspensa. Em seguida, escolha um **Grupo de recursos** ou selecione **Criar** para criar um grupo de recursos para o novo serviço de Registro do SQL Server. 
1. Em **Detalhes do Serviço**, forneça um nome e uma região para o novo recurso de **Registro do SQL Server**: 

   ![Escolha o serviço de Registro do SQL Server](media/sql-server-extended-security-updates/create-new-sql-server-registry.png)

1. Selecione **Analisar + criar** para analisar os detalhes de seu **Registro do SQL Server**. Selecione **Criar** depois que a validação tiver sido aprovada. 

## <a name="register-instances-for-esus"></a>Registrar instâncias para ESUs

Depois que o recurso de **Registro do SQL Server** for implantado, você poderá optar por registrar uma [única](#single-sql-server-instance) instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou registrar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [em massa](#multiple-sql-server-instances-in-bulk). É necessário que pelo menos uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja registrada no escopo do seu Registro do SQL Server para baixar pacotes de ESU. 

### <a name="single-sql-server-instance"></a>Instância única do SQL Server

Para registrar uma instância única do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siga estas etapas:

1. Faça logon no [Portal do Azure](https://portal.azure.com). 
1. Vá para o recurso **Registro do SQL Server**. 
1. Selecione **+ Registrar** no painel **Visão Geral**: 

   ![escolha Registrar para registrar uma instância do SQL Server](media/sql-server-extended-security-updates/register-single-sql-server-instance.png)

1. Forneça as informações necessárias conforme detalhado nesta tabela e, em seguida, selecione **Registrar**: 

   |**Valor**| **Descrição**|
   | :-------| :------------- |
   | **Instância** | insira a saída do comando `SELECT @@SERVERNAME`, como `MyServer\Instance01`. | 
   | **Versão do SQL** | Selecione 2008 ou 2008 R2 na lista suspensa. | 
   | **Edição** | Selecione a edição aplicável na lista suspensa: Datacenter, Developer (gratuito para implantar, se tiver adquirido ESUs), Enterprise, Standard, Web, Workgroup. | 
   | **Núcleos** | Insira o número de núcleos para esta instância | 
   | **Tipo de Host** | Selecione o tipo de host aplicável na lista suspensa: Máquina virtual (local), Servidor Físico (local), Máquina Virtual do Azure, Amazon EC2, Mecanismo de Computação do Google, Outro. |
   | **SubscriptionID**<sup>1</sup> | Insira a SubscriptionID em que a VM é criada.  |
   | **Grupo de Recursos**<sup>1</sup> | Insira o grupo de recursos no qual a VM é criada.  | 
   | **Nome da VM do Azure**<sup>1</sup>  | Insira o nome do recurso da VM.  | 
   | **Sistema operacional da VM do Azure**<sup>1</sup> | Selecione a versão do sistema operacional Windows Server aplicável na lista suspensa. | 

   <sup>1</sup> Necessário apenas para máquinas virtuais do Azure. 

A instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrada recentemente agora está visível na seção **Registrar instâncias do SQL Server** do painel **Visão Geral**: 

![Instâncias do SQL Server Registradas](media/sql-server-extended-security-updates/registered-sql-instance.png)

Depois que uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver sido registrada, a seção **Atualizações de Segurança** será disponibilizada. Qualquer ESUs disponível será postada lá. 

### <a name="multiple-sql-server-instances-in-bulk"></a>Várias instâncias do SQL Server em massa

Várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser registradas em massa carregando um arquivo .CSV. Quando seu [arquivo .CSV tiver sido formatado corretamente](#formatting-requirements-for-csv-file), você poderá seguir estas etapas para registrar em massa suas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o recurso de Registro do SQL Server: 

1. Faça logon no [Portal do Azure](https://portal.azure.com). 
1. Vá para o recurso **Registro do SQL Server**. 
1. Selecione **Registrar em Massa** no painel **Visão Geral**:  

   ![Escolher registro em massa para registrar várias instâncias do SQL Server](media/sql-server-extended-security-updates/bulk-register-sql-server-instances.png)

1. Selecione o ícone de arquivo para navegar até a localização do arquivo .CSV. Selecione o arquivo .CSV. Em seguida, selecione **Registrar** para carregar o arquivo e registrar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

   ![Carregar arquivo CSV para registrar várias instâncias do SQL Server](media/sql-server-extended-security-updates/upload-csv-file-for-bulk-registration.png)

### <a name="formatting-requirements-for-csv-file"></a>Requisitos de formatação para o arquivo CSV
- Os valores são separados por vírgula
- Os valores não são de aspas simples nem duplas
- Os nomes de coluna não diferenciam maiúsculas de minúsculas, mas devem ser **nomeados** como segue: 
  - name
  - version
  - edition
  - cores
  - hostType
  - subscriptionID<sup>1</sup>
  - resourceGroup<sup>1</sup>
  - azureVmName<sup>1</sup>
  - AzureVmOS<sup>1</sup>

<sup>1</sup> Necessário apenas para Máquinas Virtuais do Azure. 

#### <a name="csv-example-1---on-premises"></a>Exemplo de CSV 1 – local

Para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] locais, o arquivo CSV deve ter a seguinte aparência: 

```csv
name,version,edition,cores,hostType
Server1\SQL2008,2008,Enterprise,12,Physical Server
Server1\SQL2008R2,2008 R2,Enterprise,12,Physical Server
Server2\SQL2008R2,2008 R2,Enterprise,24,Physical Server
Server3\SQL2008R2,2008 R2,Enterprise,12,Virtual Machine
Server4\SQL2008,2008,Developer,8,Physical Server  
```

Confira [MyPhysicalServers.csv](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts/MyPhysicalServers.csv) para obter um exemplo de arquivo CSV.

#### <a name="csv-example-2---azure-vm"></a>Exemplo de CSV 2 – VM do Azure

Para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Máquina Virtual do Azure, o arquivo CSV deve ter a seguinte aparência: 

```csv
name,version,edition,cores,hostType,subscriptionId,resourceGroup,azureVmName,azureVmOS    
ProdServerUS1\SQL01,2008 R2,Enterprise,12,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM1,2012    
ProdServerUS1\SQL02,2008 R2,Enterprise,24,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM1,2012    
ServerUS2\SQL01,2008,Enterprise,12,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM2,2012 R2    
ServerUS2\SQL02,2008,Enterprise,8,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM2,2012 R2    
SalesServer\SQLProdSales,2008 R2,Developer,8,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM3,2008 R2  
```

Confira [MyAzureVMs.csv](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts/MyAzureVMs.csv) para obter um exemplo de arquivo CSV almejado da VM do Azure. 


> [!TIP]
> Para scripts de exemplo do PowerShell e do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem gerar as informações de registro de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necessárias em um arquivo .CSV, confira [Exemplos de script de registro da ESU](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts.md). 

## <a name="download-esus"></a>Baixar ESUs

Depois que suas instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiverem sido registradas com o serviço de Registro do SQL Server, você poderá baixar os pacotes de Atualizações de Segurança Estendidas usando o link encontrado no portal do Azure, se e quando forem disponibilizados. 

Para baixar as ESUs, siga estas etapas: 

1. Faça logon no [Portal do Azure](https://portal.azure.com). 
1. Vá para o recurso **Registro do SQL Server**. 
1. Selecione **Atualizações de Segurança** no painel de navegação. 

   ![Verificar atualizações disponíveis no o painel atualizações de segurança](media/sql-server-extended-security-updates/security-updates-sql-registry.png)

1. Baixe as atualizações de segurança aqui, se e quando elas forem disponibilizadas. 

## <a name="configure-regional-redundancy"></a>Configurar redundância regional 

Os clientes que exigem redundância regional para seus **registros do SQL Server** podem criar dados de registro em duas regiões distintas. Os clientes podem, então, baixar atualizações de segurança de qualquer região com base na disponibilidade do serviço de **registro do SQL Server**. 

Para redundância regional, um serviço de **registro do SQL Server** precisa ser criado em duas regiões diferentes, e seu inventário do SQL Server precisa ser dividido entre esses dois serviços. Dessa forma, metade dos seus SQL Servers são registrados com o serviço de registro em uma região, e a outra metade é registrada com o serviço de registro na outra região. 

Para configurar a redundância regional, siga estas etapas:

1. Divida o inventário do SQL Server 2008 ou 2008 R2 em dois arquivos, como upload1.csv e upload2.csv. 
  
   :::image type="content" source="media/sql-server-extended-security-updates/two-upload-files-for-regional-redundancy.png" alt-text="Exemplo de arquivos de upload":::

1. Crie o primeiro serviço de **registro do SQL Server** em uma região e, em seguida, registre em massa um dos arquivos csv nele. Por exemplo, crie o primeiro serviço de **registro do SQL Server** na região **Oeste dos EUA** e registre em massa seus SQL Servers usando o arquivo upload1.csv. 
1. Crie o segundo serviço de **registro do SQL Server** na segunda região e, em seguida, registre em massa o outro arquivos csv nele. Por exemplo, crie o segundo serviço de **registro do SQL Server** na região **Leste dos EUA** e registre em massa seus SQL Servers usando o arquivo upload2.csv. 


Depois que seus dados forem registrados com os dois recursos diferentes de **registro do SQL Server**, você poderá fazer baixar as atualizações de segurança de qualquer região, com base na disponibilidade do serviço. 


## <a name="faq"></a>Perguntas frequentes

As perguntas mais frequentes sobre Atualizações de Segurança Estendidas podem ser encontradas nas [Perguntas frequentes sobre atualizações de segurança estendidas](https://www.microsoft.com/cloud-platform/extended-security-updates). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-as perguntas frequentes específicas são listadas abaixo. 

**Quando ocorreu o fim do suporte para o SQL Server 2008 e o SQL Server 2008 R2?**

A data de fim do suporte para o [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e o [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] foi 9 de julho de 2019. 

**O que significa fim do suporte?**

A política de ciclo de vida da Microsoft oferece dez anos de suporte (cinco anos para suporte base e cinco anos para suporte estendido) para produtos empresariais e para desenvolvedores (como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows Server). De acordo com a política, após o término do período de suporte estendido, não haverá patches ou atualizações de segurança, o que pode causar problemas de segurança e conformidade e expor os aplicativos dos clientes e as empresas a sérios riscos de segurança.

**Quais edições do SQL Server estão qualificadas para Atualizações de Segurança Estendidas?**

As edições Enterprise, Datacenter, Standard, Web e Workgroup do [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e do [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] são elegíveis para Atualizações de Segurança Estendidas para versões x86 e x64. 

**Quando a oferta de Atualizações de Segurança Estendidas estará disponível?**

As Atualizações de Segurança Estendidas agora estão disponíveis para compra e podem ser pedidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou de um parceiro de licenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)]. A entrega de Atualizações de Segurança Estendidas será iniciada após o término das datas de suporte, se e quando disponíveis. Os clientes interessados em migrar para o Azure podem fazer isso imediatamente. 

**O que as Atualizações de Segurança Estendidas incluem?** 

As Atualizações de Segurança Estendidas incluem o provisionamento de atualizações de segurança e Boletins classificados como **críticos** pelo [MSRC (Microsoft Security Response Center)](https://portal.msrc.microsoft.com/) por um máximo de três anos após 9 de julho de 2019. As Atualizações de Segurança Estendidas serão distribuídas se e quando disponíveis. As Atualizações de Segurança Estendidas não incluem suporte técnico, mas você pode usar outros planos de suporte [!INCLUDE[msCoName](../../includes/msconame-md.md)] para obter assistência para suas questões de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] sobre cargas de trabalho cobertas por Atualizações de Segurança Estendidas. as Atualizações de Segurança Estendida não incluem novos recursos, aprimoramentos funcionais nem correções solicitadas pelo cliente. No entanto, [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode incluir correções não relacionadas à segurança, conforme considerado necessário.

**Por que as Atualizações de Segurança Estendidas para o SQL Server 2008 e o SQL Server 2008 R2 oferecem apenas atualizações "críticas"?**

Para os eventos de fim do suporte no passado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecia apenas atualizações de segurança críticas, que cumprem os critérios de conformidade de nossos clientes empresariais. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não envia uma atualização de segurança mensal geral. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] só fornece atualizações de segurança (GDRs) sob demanda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para boletins do MSRC em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é identificado como um produto afetado.
Se houver situações em que novas atualizações importantes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não serão fornecidas e elas forem consideradas críticas pelo cliente, mas não pelo MSRC, trabalharemos com o cliente caso a caso para sugerir a mitigação apropriada.

**Quais programas de licenciamento são elegíveis para Atualizações de Segurança Estendidas?**

Os clientes do Software Assurance podem comprar Atualizações de Segurança Estendidas localmente em um EA (Contrato Enterprise), EAS (Contrato Enterprise Subscription), SCE (Registro de Servidor e Nuvem) ou EES (Registro para Soluções de Educação). O Software Assurance não precisa estar no mesmo registro.

**Os clientes do SQL Server precisam estar executando o Service Pack mais recente para beneficiarem-se das Atualizações de Segurança Estendidas?**

Sim, os clientes precisam executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Windows Server 2008 e 2008 R2 com o Service Pack mais recente para aplicar Atualizações de Segurança Estendidas. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] só produzirá atualizações que possam ser aplicadas ao Service Pack mais recente.

**Quais são as opções para clientes do SQL Server sem Software Assurance?** 

Para clientes que não têm o Software Assurance, a opção alternativa para obter acesso a Atualizações de Segurança Estendidas é migrar para o Azure. Para cargas de trabalho variáveis, recomendamos que os clientes migrem no Azure por meio de Pagamento Conforme o Uso, o que permite expandir ou reduzir a qualquer momento. Para cargas de trabalho previsíveis, recomendamos que os clientes migrem para o Azure usando a Assinatura de Servidor e Instâncias Reservadas.
  
**Essa oferta também se aplica ao SQL Server 2005?**

Não. Para essas versões mais antigas, é recomendável atualizar para as versões mais recentes, mas os clientes podem atualizar para versões [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] ou [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] para aproveitar essa oferta.

**Posso implantar uma instância totalmente nova do SQL Server 2008 ou 2008 R2 no Azure e ainda obter Atualizações de Segurança Estendidas?**

Sim, os clientes podem iniciar uma nova instância do [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] ou do [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] em uma Máquina Virtual do Azure e ter acesso a Atualizações de Segurança Estendidas.

**Posso obter suporte técnico local para o SQL Server 2008 ou 2008 R2 após a data de término do suporte sem comprar Atualizações de Segurança Estendidas?**

Não. Se um cliente tiver [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] ou [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] e optar por permanecer local durante uma migração sem Atualizações de Segurança Estendidas, ele não poderá registrar um tíquete de suporte, mesmo que tenha um plano de suporte. No entanto, se ele migrar para o Azure, poderá obter suporte usando o Plano de Suporte do Azure.

**Se um cliente do SQL Server 2008 e do 2008 R2 quiser usar a opção BYOL (traga sua própria licença), eles deverá ter cobertura do Software Assurance?**

Sim, os clientes precisam ter o Software Assurance para aproveitar o programa BYOL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em máquinas virtuais do Azure como parte do programa Mobilidade de Licenças. Para clientes sem Software Assurance, recomendamos migrar para a Instância Gerenciada do Banco de Dados SQL do Azure para seus ambientes do [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]. Os clientes também podem migrar para máquinas virtuais do Azure pagas conforme o uso. Os clientes do Software Assurance que licenciam o SQL por núcleo também têm a opção de migrar para o Azure usando o AHB (Benefício Híbrido do Azure).

A Instância Gerenciada do Banco de Dados SQL do Azure é um serviço no Azure que fornece quase 100% de compatibilidade com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local. A Instância Gerenciada fornece recursos internos de alta disponibilidade/recuperação de desastres, além de recursos de desempenho inteligente e a capacidade de dimensionar em tempo real. A Instância Gerenciada também fornece uma experiência sem versões que elimina a necessidade de atualização e aplicação de patches de segurança manuais. Confira a página de diretrizes de preços do Azure para obter mais informações sobre o programa BYOL.

**Quais opções os clientes têm para executar o SQL Server no Azure?**

Os clientes podem mover ambientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herdados para Instância Gerenciada do Banco de Dados SQL do Azure, um serviço de plataforma de dados totalmente gerenciado (PaaS) que oferece uma opção de "sem versão" para eliminar as preocupações com o fim das datas de suporte ou para que as máquinas virtuais do Azure tenham acesso às atualizações de segurança. Os bancos de dados migrados reterão a compatibilidade com o sistema herdado. Para saber mais, confira [Certificação de Compatibilidade](../../database-engine/install-windows/compatibility-certification.md).

As atualizações de segurança estendidas estarão disponíveis para [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] em Máquinas Virtuais do Azure após o fim da data de suporte de 9 de julho de 2019 pelos próximos três anos. Para clientes que procuram atualizar de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)], todas as versões subsequentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão compatíveis. Para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], os clientes precisam estar no Service Pack mais recente compatível. Do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] em diante, é aconselhável que os clientes estejam na atualização cumulativa mais recente. Observe que os Service Packs não estarão disponíveis do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] em diante, somente atualizações cumulativas e GDRs (versões de distribuição geral).

A Instância Gerenciada do Banco de Dados SQL do Azure é uma opção de implantação com escopo de instância no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] que fornece a maior compatibilidade de mecanismo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e suporte nativo para VNET (rede virtual) para que você possa migrar bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a Instância Gerenciada sem mudar de aplicativo. Ela combina a ampla área de superfície do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com os benefícios operacionais e financeiros de um serviço inteligente e totalmente gerenciado. Aproveite o novo Serviço de Migração de Banco de Dados do Azure para mover [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] para a Instância Gerenciada do Banco de Dados SQL do Azure com pouca ou nenhuma alteração de código do aplicativo.

**Os clientes podem aproveitar o Benefício Híbrido do Azure para as versões SQL Server 2008 e 2008 R2?**

Sim, os clientes com Software Assurance ativo ou assinaturas de servidor equivalentes podem aproveitar o Benefício Híbrido do Azure usando os investimentos em licença local existentes para preços com desconto no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em máquinas virtuais do Azure e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

**Os clientes podem obter Atualizações de Segurança Estendidas gratuitas nas regiões do Azure Government?**

Sim, as Atualizações de Segurança Estendidas estarão disponíveis em máquinas virtuais do Azure nas regiões do Azure Government.

**Os clientes podem obter Atualizações de Segurança Estendidas gratuitas no Azure Stack?**

Sim, os clientes podem migrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Windows Server 2008 e [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] para Azure Stack e receber Atualizações de Segurança Estendidas sem custo adicional após o fim das datas de suporte.

**Para clientes com um cluster do SQL 2008 e 2008 R2 usando armazenamento compartilhado, qual é a orientação para migrar para o Azure?**

No momento, o Azure não é compatível com clustering de armazenamento compartilhado. Para obter conselhos sobre como configurar uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] altamente disponível no Azure, confira o [Guia de Alta Disponibilidade do SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr).

**Os clientes podem aproveitar as Atualizações de Segurança Estendidas para SQL Server com um hoster de terceiros?**

Os clientes não poderão aproveitar as atualizações de segurança estendidas se levarem o ambiente de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] para uma implementação de PaaS em outros provedores de nuvem. Se os clientes estiverem procurando migrar para máquinas virtuais (IaaS), eles poderão utilizar a Mobilidade de Licenças para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do Software Assurance para fazer a movimentação e comprar Atualizações de Segurança Estendidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para aplicar patches manualmente às instâncias de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] em execução em uma VM (IaaS) em um servidor do hoster SPLA autorizado. No entanto, as atualizações gratuitas no Azure são a oferta mais atraente.

**Quais são as melhores práticas para melhorar o desempenho do SQL Server em máquinas virtuais do Azure?** 

Para obter conselhos sobre como otimizar o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em máquinas virtuais do Azure, confira o [Guia de otimização do SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance). 

## <a name="see-also"></a>Confira também

- [Página do ciclo de vida do SQL Server 2008/2008 R2](https://support.microsoft.com/lifecycle/search?alpha=sql%20server%202008)
- [Página de fim do suporte do SQL Server 2008/2008 R2](https://aka.ms/sqleos)
- [Perguntas frequentes sobre Atualizações de Segurança Estendidas](https://aka.ms/sqleosfaq)
- [Microsoft Security Response Center (MSRC)](https://portal.msrc.microsoft.com/security-guidance/summary)
- [Gerenciar atualizações do Windows com a Automação do Azure](/azure/automation/automation-tutorial-update-management)
- [Aplicação de patch automatizada da VM do SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)
- [Guia de migração de dados da Microsoft](https://datamigration.microsoft.com/)
- [Migrações para Azure: opções de lift-and-shift para mover seu SQL Server 2008/2008 R2 atual para uma VM do Azure](https://azure.microsoft.com/services/azure-migrate/)
- [Cloud Adoption Framework para migração do SQL](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)
- [Scripts relacionados a ESU no GitHub](https://github.com/microsoft/sql-server-samples/tree/master/samples/manage/sql-server-extended-security-updates/scripts)

