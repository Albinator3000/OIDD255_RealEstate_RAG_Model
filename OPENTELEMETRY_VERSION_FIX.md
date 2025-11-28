# OpenTelemetry Version Fix

## Issue
The project was initially using both OpenTelemetry 1.37.0 and 1.38.0 versions inconsistently across dependencies, causing potential compatibility issues.

## Solution
All OpenTelemetry packages have been pinned to version **1.37.0** throughout the entire project.

## Changes Made

### 1. Updated `requirements.txt`
Added explicit version pins for all OpenTelemetry packages:
```
opentelemetry-api==1.37.0
opentelemetry-sdk==1.37.0
opentelemetry-exporter-otlp-proto-common==1.37.0
opentelemetry-exporter-otlp-proto-grpc==1.37.0
opentelemetry-proto==1.37.0
opentelemetry-semantic-conventions==0.58b0
```

### 2. Updated `requirements_simple.txt`
Added the same OpenTelemetry version pins to the simplified requirements file.

### 3. Created `constraints.txt`
New file that enforces these version constraints for future installations.

### 4. Updated `real_estate_due_diligence_COLAB.ipynb`
Updated the pip install command in cell 2 to pin OpenTelemetry versions when running in Google Colab.

### 5. Local Environment Updated
Downgraded existing OpenTelemetry packages from 1.38.0 to 1.37.0 in the virtual environment.

## Why Version 1.37.0?
- Compatible with existing ChromaDB and LangChain dependencies
- `opentelemetry-sdk==1.37.0` requires `opentelemetry-semantic-conventions==0.58b0`
- Consistent across all environments (local and Colab)

## Verification
Run this command to verify all versions are correct:
```bash
source venv/bin/activate
pip list | grep -i opentelemetry
```

Expected output:
```
opentelemetry-api                        1.37.0
opentelemetry-exporter-otlp-proto-common 1.37.0
opentelemetry-exporter-otlp-proto-grpc   1.37.0
opentelemetry-proto                      1.37.0
opentelemetry-sdk                        1.37.0
opentelemetry-semantic-conventions       0.58b0
```

## Future Installations
To ensure the correct versions are always installed, use:
```bash
pip install -r requirements_simple.txt
```

The constraints are now enforced in all requirements files, preventing accidental upgrades to 1.38.0.

## Note on semantic-conventions
The `opentelemetry-semantic-conventions` version (0.58b0) is determined by the `opentelemetry-sdk==1.37.0` dependency. This is correct and should not be changed independently.
