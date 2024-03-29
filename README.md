<h1 align="center">
	DataHowdah ✨🔒🔢✨
</h1>
<p align="center">
  <em>DataHowdah: Effortlessly mask and 🔐 encrypt your data frames, ensuring their safety like a camel's secure howdah 🐪</em>
</p>
<p align="center">
  <img alt="" style="border-radius: 8px" src="https://badge.fury.io/py/data-howdah.svg"/>
</p>

![1704128527248](https://github.com/mustafah/data-howdah/raw/main/images/README/caravan2.jpeg)

# DataHowdah ✨🔒🔢✨

DataHowdah is a utility python class designed to mask or encrypt pandas data frames while sharing them on different machines. It extends the functionality of pandas DataFrames, offering encryption and noise addition features for sensitive data columns. By using plain simple passwords or integrating with Microsoft Azure Key Vault (and AWS KMS), DataHowdah ensures that encryption keys are managed securely and efficiently. Its intuitive interface allows for seamless encryption and decryption of DataFrame columns, safeguarding data as it travels between systems.

```python
from data_howdah import DataHowdah

df = DataHowdah('sample.csv')
df.encrypt(['secret_column_1', 'secret_column_2'])
df.to_csv('encrypted_data.csv', index=False)
```

## **🌱 How to Begin**

* 💻 Install :

```bash
pip install data-howdah
```

* 🔑 Environment variables may contain your either your simple Encryption Key :

```bash
DATA_HOWDAH_ENCRYPTION_KEY=
```

or your AZURE KEY VAULT secret url:

```bash
DATA_HOWDAH_AZURE_KEY_VAULT_SECRET_URL=https://{key-vault-name}.vault.azure.net/{secret_name}
```

Don't forget to install Azure CLI and login successfully

```bash
az login
```

AWS KMS (coming soon!)

* 📈 Create or load your dataframe and pass it to DataHowdah:

```python
import pandas as pd
import numpy as np

# load directly from file, supports popular file paths
df = DataHowdah('sample.csv')
# or pass to it a dataframe object
df = DataHowdah(pd.DataFrame(np.random.rand(100, 3), columns=['A', 'B', 'C']))
```

    ℹ️ DataHowdah is derived class from pd.DataFrame, so you can deal with as a regular dataframe

* 🎭 Mask :

The mask method adds statistical noise to numeric columns in a DataFrame, effectively disguising the original data while preserving its overall structure and distribution.

```python
from data_howdah import DataHowdah

df = DataHowdah('sample.csv')
df.mask([0], scale = 0.5, plot = True)

# Params :
# scale: Adjusts the intensity of noise added to numeric data, with higher values increasing data obfuscation.
# plots: When set to True, generates comparative visualizations of original and masked data distributions.

df.to_csv('masked_data.csv', index=False) # Save it in the format you like !
```

* 🔒 Encrypt :

The encrypt method in DataHowdah securely transforms specified columns in a DataFrame into unreadable formats, safeguarding sensitive information.

```python
from data_howdah import DataHowdah

df = DataHowdah('sample.csv')
df.encrypt(['secret_column', 1, slice(5, 8)])

# Params :
# 1. columns_to_encrypt: Specifies which DataFrame columns to secure, accepting column names, indices, or slices.
# 2. key: The encryption key used for data protection.

df.to_csv('encrypted_data.csv', index=False) # Save it in the format you like !
```

* 🔓 Decrypt :

The decrypt method in DataHowdah reverses the encryption of the pre-encrypted columns, it auto detects these columns

```python
from data_howdah import DataHowdah

df = DataHowdah('encrypted_data.csv')
df.decrypt()

df.to_csv('decrypted_data.csv', index=False) # Save it in the format you like !
```
