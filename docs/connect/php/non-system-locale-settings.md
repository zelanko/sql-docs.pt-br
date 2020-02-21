---
title: Configurações de localidade que não pertencem ao sistema | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: bd60bff3ab9ee19b1a1d2435e69651ea054689e7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76913319"
---
# <a name="non-system-locale-settings"></a>Configurações de localidade que não pertencem ao sistema
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta seção se aplica somente aos usuários do Linux e do macOS, especialmente aqueles que lidam com mais de uma localidade nos aplicativos PHP.

Por padrão, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] usa a variável de ambiente `LC_ALL` definida no sistema e substitui todas as outras categorias `LC_xxx` (exceto `$LANG` ou `$LANGUAGE` em algumas circunstâncias), afetando o separador de milhares, o caractere de ponto decimal, o conjunto de caracteres,o mês, os nomes dos dias, as mensagens de aplicativo, como mensagens de erro, o símbolo de moeda etc.

Com a versão 5.8.0, os usuários podem definir as configurações de localização usando o arquivo php.ini, conforme mostrado nos exemplos abaixo.

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>Definir informações de localidade usando o Driver SQLSRV  
Adicione o seguinte ao final do arquivo php.ini:
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>Definir informações de localidade usando o Driver PDO_SQLSRV  
Adicione o seguinte ao final do arquivo php.ini:
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
A **opção** pode ser um dos seguintes valores:  
  
|Opção|Descrição do comportamento|
|---------|---------------|
|0|O driver ignora as configurações de localidade do sistema.|
|1|O driver lê a variável LC_CTYPE.|
|2|O driver lê a variável LC_ALL (esse é o padrão).|
  

A categoria `LC_CTYPE` determina as regras de manipulação de caracteres, que regem a interpretação de sequências de bytes de caracteres de dados de texto, a classificação de caracteres e o comportamento das classes de caracteres. Ele controla o reconhecimento de caracteres maiúsculos e minúsculos, alfabéticos e não alfabéticos e assim por diante.

### <a name="explanation"></a>Explicação

1. Opção 0 – use quando não quiser alterar a localidade do aplicativo.

1. Opção 1 – use para definir somente o valor do sistema de `LC_CTYPE` sem afetar outras categorias `LC_xxx`.

1. Opção 2 – use `LC_ALL` para substituir todas as categorias `LC_xxx`, afetando o aplicativo PHP e as extensões dele.

Caso a localidade de qualquer script php não seja a mesma do sistema, talvez seja necessário especificar a localidade nos scripts(s) php chamando a função interna [setlocale](https://www.php.net/manual/en/function.setlocale.php) do php. 

Por exemplo, caso o padrão do sistema seja `en_US.UTF-8`, mas o script php use `de_DE.UTF-8`, então chame a função php `setlocale()` de maneira apropriada.

Para a Opção 2, indique a localidade desejada em seus scripts php somente no caso em que ela for diferente da variável `LC_ALL`.

> [!NOTE]
> Caso nada seja definido em php.ini, o padrão atual é substituir todas as outras configurações de localidade com base em `LC_ALL` que serão **preteridas**. Em breve, o padrão será ignorar as configurações de localidade do sistema. Portanto, os usuários precisarão modificar o arquivo php.ini de maneira adequada caso queiram manter o comportamento atual.

Caso os drivers sqlsrv e pdo_sqlsrv estejam habilitados, não será recomendado configurar opções diferentes para eles.