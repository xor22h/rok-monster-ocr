# Rise of Kingdoms OCR Tools

[![Discord](https://img.shields.io/discord/768180228710465598)](https://discord.gg/drhxwVQ) [![License: MIT](https://img.shields.io/github/license/carmelosantana/rok-monster-ocr)](https://opensource.org/licenses/MIT)

- [Rise of Kingdoms OCR Tools](#rise-of-kingdoms-ocr-tools)
  - [RoK Monster OCR](#rok-monster-ocr)
  - [How it works](#how-it-works)
  - [Install](#install)
    - [Automated](#automated)
    - [Manual](#manual)
      - [Software](#software)
      - [Tessdata](#tessdata)
      - [rok-monster-ocr](#rok-monster-ocr-1)
  - [Usage](#usage)
    - [Start a job via CLI](#start-a-job-via-cli)
  - [Arguments](#arguments)
  - [Community](#community)
  - [Funding](#funding)
  - [License](#license)

---

📢 Please join our [Discord](https://discord.gg/drhxwVQ) to stay current on recent changes.

<center>

🌟 Inquire about **premium support**.🌟

</center>

---

## [RoK Monster OCR](https://rokmonster.com)

Command line tools to generate player statistics from [Rise of Kingdoms](https://rok.lilithgames.com/en). By analyzing screenshots we can extract various data points such as governor power, deaths, kills and more. This can help with various kingdom statistics or fairly distributing [KvK](https://rok.guide/the-lost-kingdom-kvk/) rewards.

![Sample](https://carmelosantana.com/app/uploads/2020/11/rok-monster-cli-v0.2.0.png)

*Results may vary.*

## How it works

Quick overview of the expected process when executing the job `governor-more-info-kills`.

1. **rok-monster-ocr** will iterate through each screenshot and compare the input image to a known fingerprint of the image containing data to capture.
2. If a match is made the image is prepared per the instructions declared in the OCR profile. *Each cropped segment represents a single data point.*
   - This process is repeated for each image in the `input_path`.
3. By default on completion a table is printed via CLI and a CSV file is saved in the current working directory.

> 📌 Input path can be defined in `.env` file or via CLI argument `--input_path`.

## Install

### Automated

One line install.

```bash
curl -sSL https://raw.githubusercontent.com/carmelosantana/rok-monster-ocr/master/install.sh | bash -s y
```

This will install all necessary dependencies and start a small demo project.

---

Alternatively you can clone the repository and review the install script before executing.

```bash
git clone https://github.com/carmelosantana/rok-monster-ocr/
cd rok-monster-ocr
sudo bash install.sh
```

### Manual

Requirements:

- [PHP](https://www.php.net/manual/en/install.php) 7.4
  - GD extension
- [Composer](https://getcomposer.org/)
- [ImageMagick](https://imagemagick.org/)
- [Tesseract](https://github.com/tesseract-ocr/tesseract)
- [FFmpeg](https://ffmpeg.org/) *(Only required if you plan on processing videos)*

#### Software

This assumes you have [PHP](https://www.php.net/manual/en/install.php) installed with access to [Composer](https://getcomposer.org/).

```bash
sudo apt install imagemagick ffmpeg tesseract-ocr
```

*This does not represent the complete install instructions for all dependencies. Please review the [install script](https://github.com/carmelosantana/rok-monster-ocr/blob/master/install.sh) for detailed installation instructions.*

#### Tessdata

Using [tessdata](https://github.com/tesseract-ocr/tessdata) or [tessdata_best](https://github.com/tesseract-ocr/tessdata_best) models from the [Tesseract](https://github.com/tesseract-ocr) repositories have produced better results than the models provided by `apt-get`. You can download select languages or clone the repository and set this path with in the `.env` file or via CLI argument `--tessdata`.

Alternatively you can install via `apt-get`. Some issues may include:

- Incorrect user permissions
- Models don't work with legacy engine
- Can be less accurate

```bash
sudo apt install tesseract-ocr-all
```

#### rok-monster-ocr

```bash
git clone https://github.com/carmelosantana/rok-monster-ocr
cd rok-monster-ocr
composer install
```

## Usage

- Game resolution and capture of at least 1920x1080.
- English language is preferred as coordinate information lines up most accurately with English.
- Move all images to your "Input Path" as defined in your `.env` file or via CLI argument `--input_path`.
  - By default a "Media" folder is created in your current working directory if no directory is supplied.

## Docker usage

- Read [docker.md](./docker.md)

### Start a job via CLI

1. Capture the necessary screens specified per the given job. In this example we need the **Governor More Info** profile screen.
2. Run job:

    ```bash
    php rok.php --job=governor-more-info-kills --input_path=DIR_WITH_SCREENSHOTS
    ```

3. Check your current working directory for any output files.

## Arguments

| Argument | Value | Default | Description |
| --- | --- | --- | --- |
| debug | `bool` | `0` | Prints raw OCR reading per image. Uses local `--tmp_path` and preserves cropped images. |
| job | `string` | *Required* | Name of job defined as defined in [rok-monster-schema](https://github.com/carmelosantana/rok-monster-schema) |
| input_path | `string` | *Required* | Media source path or file  |
| tmp_path | `string` | `sys_get_temp_dir()`| Temp directory for images manipulated during processing  |
| oem | `int` | `0` | OCR Engine Mode |
| psm | `int` | `0` | Page Segmentation Method |
| tessdata | `string` | `null` | User defined location for tessdata. Defaults to system installation path.  |
| compare_to_sample | `bool` | `1` | Enable compare to sample  |
| video | `bool` | `1` | Enable video processing |

- *bool as `0\1` or `true\false` or `on\off`*

## Community

Have a question, an idea, or need help getting started? Checkout our [Discord](https://discord.gg/drhxwVQ)!

Honorable mentions for [community](https://discord.gg/drhxwVQ) members who've donated time and resources to **rok-monster-ocr** or [rokmonster.com](https://rokmonster.com).

- BouchB
- j7johnny
- Star Lordツ

## Funding

If you find **rok-monster-ocr** useful you can help fund future development by making a contribution to one of our funding sources below.

- [PayPal](https://www.paypal.com/donate?hosted_button_id=EKK8CQTPJG7WL)
- Bitcoin `bc1qx7v5vvxwnhpl3dssggy0hytcx2rpq5dkkfwyy4`
- Ethereum `0xA8Ebb6e5EC503E90551dD1bdE2d00B6C126eD5C5`
- Tron `TPnGEfkUZ2py6CFkh8wgqqYehJ29EbMWVw`

## License

The code is licensed [MIT](https://opensource.org/licenses/MIT) and the documentation is licensed [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
