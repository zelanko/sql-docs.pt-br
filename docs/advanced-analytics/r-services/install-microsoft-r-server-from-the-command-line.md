---
title: "Instalar o Microsoft R Server na Linha de comando | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# Instalar o Microsoft R Server na Linha de comando
    
Você pode instalar o Microsoft R Server na linha de comando usando os recursos de scripts fornecidos com a instalação do SQL Server. 

- A instalação **Autônoma** exige que você especifique o local do utilitário de instalação e use argumentos para indicar quais recursos serão instalados. 
- Para uma instalação **silenciosa**, forneça os mesmos argumentos e adicione o switch **/q**. Nenhum aviso será fornecido e não é necessária nenhuma interação. No entanto, a instalação falhará se os argumentos necessários forem omitidos.

Para obter mais informações, consulte [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="perform-a-commandline-install-of-microsoft-r-server-standalone"></a>Executar uma instalação de linha de comando do Microsoft R Server (Autônomo)

 Os exemplos a seguir mostram os argumentos usados ao executar uma instalação de linha de comando do Microsoft R Server usando a instalação do SQL Server.


### <a name="example-of-unattended-installation-of-r-server-standalone"></a>Exemplo de uma instalação autônoma de um R Server Autônomo

Execute o seguinte comando, em um prompt de comandos com privilégios elevados, para instalar somente o Microsoft R Server (Autônomo) e seus pré-requisitos. 

```  
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```  

Para exibir o progresso e as solicitações, remova o argumento /q.

Observe que todos os argumentos a seguir são necessários:
  - **FEATURES = SQL_SHARED_MR** obtém somente os componentes do Microsoft R Server, incluindo o Microsoft R Open e todos os pré-requisitos.
  - **IACCEPTROPENLICENSETERMS** indica que você aceitou os termos de licença para usar os componentes de software livre do R.
  - **IACCEPTSQLSERVERLICENSETERMS** é necessário para executar o assistente de instalação.


### <a name="offline-installation"></a>Instalação offline

Se você instalar o Microsoft R Server (Autônomo) em um computador sem acesso à Internet, você deve antes baixar os componentes necessários do R e copiá-los em uma pasta local. Para locais de download, consulte [Instalando componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).   


## <a name="advanced-installation-tips"></a>Dicas de instalação avançadas

Após a conclusão da instalação, você pode examinar o arquivo de configuração criado pela instalação do SQL Server, juntamente com um resumo das ações de instalação.

Por padrão, todos os logs e resumos de instalação do SQL Server e dos recursos relacionados são criados em `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`.

Uma subpasta separada é criada para cada recurso instalado. Para o Microsoft R Server, procure: 
- `RSetup.log`
- `Settings.xml`
- `Summmary<instance_GUID>.txt`

Para configurar a outra instância do Microsoft R Server com os mesmos parâmetros, você também pode reutilizar o arquivo de configuração criado durante a instalação. Para obter mais informações sobre [Instalar o SQL Server usando um arquivo de configuração](https://msdn.microsoft.com/library/dd239405.aspx)



### <a name="customizing-your-r-environment"></a>Personalizando o ambiente do R

Após a instalação, você pode instalar pacotes do R adicionais. Para obter mais informações, consulte [Instalando e Gerenciando pacotes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

> [!IMPORTANT]
> Se você pretende executar seu código R no SQL Server, certifique-se de instalar os mesmos pacotes tanto no computador cliente executando o Microsoft R Server quanto na instância do SQL Server que esteja executando serviços de R. 



## <a name="see-also"></a>Consulte também  

[Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)
  