Discussion from last week's 10/26 STAR S&C meeting looked at the proposed design & layout of the [RHICf data structures](https://drupal.star.bnl.gov/STAR/system/files/STARSC20221026_RHICf_data_structure.pdf).  During production they propose to do full energy reconstruction (-=ped; /=gain) on each detector element.  Few points were raised:
- This would require calibrations to be known at the time of the data production
- This would require *final* calibrations to be known at that time... otherwise
	- Subsequant production would be required if/when new peds / gains / masks available
	- Having calibrated data inside the data structures risks 